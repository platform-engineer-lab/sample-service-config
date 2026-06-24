# Manifest Hydration

To hydrate the manifests in this repository, run the following commands:

```shell
git clone https://github.com/platform-engineer-lab/sample-service-config
# cd into the cloned directory
git checkout 31607ec06a184ce8d79bac190235caf982e18807
helm template . --name-template sample-service --namespace sample-service --values ./chart/env/prod/values.yaml --include-crds
```
