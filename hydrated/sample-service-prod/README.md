# Manifest Hydration

To hydrate the manifests in this repository, run the following commands:

```shell
git clone https://github.com/platform-engineer-lab/sample-service-config
# cd into the cloned directory
git checkout 42ba0cc6af0e7f361853d9a94a92829f778a29c1
helm template . --name-template sample-service --namespace business-apps --values ./chart/env/prod/values.yaml --include-crds
```
