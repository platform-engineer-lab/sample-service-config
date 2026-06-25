# Manifest Hydration

To hydrate the manifests in this repository, run the following commands:

```shell
git clone https://github.com/platform-engineer-lab/sample-service-config
# cd into the cloned directory
git checkout f30e3b93ae7f1d9112f03f7ee1940d095539df18
helm template . --name-template sample-service --namespace sample-service --values ./chart/env/prod/values.yaml --include-crds
```
