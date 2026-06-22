# sample-service-config

Helm chart + values for `sample-service`. This is the **dry source** repo watched by
gitops-promoter; CI from `sample-service` opens PRs here to bump the image tag, and
the promoter drives those changes through dev → prod via pull requests.

## Branch model

| Branch | Role | Who touches it |
|---|---|---|
| `main` | Dry source — Helm chart + values | Authors / CI |
| `env/dev-next` | Hydrated proposals for dev | Argo CD Source Hydrator |
| `env/dev` | Active dev delivery | gitops-promoter (merges `env/dev-next`) |
| `env/prod-next` | Hydrated proposals for prod | Argo CD Source Hydrator |
| `env/prod` | Active prod delivery | gitops-promoter (merges `env/prod-next`) |

`env/*-next` and `env/*` branches are managed automatically. Do **not** delete them
on PR merge — configure the repo to disable branch auto-deletion or add branch
protection rules matching `env/*-next`.

## Promotion flow

```
main (image tag bump PR merged)
  → Argo CD hydrator writes rendered manifests → env/dev-next
  → gitops-promoter opens PR env/dev-next → env/dev
  → Argo CD syncs env/dev (dev spoke), ArgoCD health = healthy
  → gitops-promoter opens PR env/prod-next → env/prod
  → Argo CD syncs env/prod (prod spoke)
```

## Required secrets (manual — not in git)

### 1. GitHub App for gitops-promoter (in `promoter-system` on the management cluster)

Create a GitHub App with:
- **Contents:** read/write
- **Pull requests:** read/write
- **Commit statuses:** write

Install it on this repo (`sample-service-config`) and on `sample-service`.
Note the `appID` and `installationID`, then:

```bash
kubectl --context k3d-management create secret generic github-app-credentials \
  --namespace promoter-system \
  --from-literal=githubAppPrivateKey="$(cat /path/to/private-key.pem)"
```

Update `platform-addons/manifests/gitops-promoter/scm-provider.yaml` with the real
`appID` (and optionally `installationID`), then push to trigger Argo CD sync.

### 2. Argo CD repo write credential (hydrator pushes to `env/*-next`)

The Argo CD Source Hydrator needs write access to this repo to push hydrated manifests.
Create a repository Secret in the `argocd` namespace on the management cluster:

```bash
kubectl --context k3d-management apply -f - <<EOF
apiVersion: v1
kind: Secret
metadata:
  name: repo-sample-service-config
  namespace: argocd
  labels:
    argocd.argoproj.io/secret-type: repository
stringData:
  url: https://github.com/platform-engineer-lab/sample-service-config
  username: git
  password: <github-pat-with-contents-write>
EOF
```

### 3. CI PAT in `sample-service` repo

Add a fine-grained PAT as `CONFIG_REPO_TOKEN` in `sample-service`'s repo secrets
(see `sample-service/README.md`).

## Local chart validation

```bash
helm template sample-service chart -f chart/env/dev/values.yaml
helm template sample-service chart -f chart/env/prod/values.yaml
```
