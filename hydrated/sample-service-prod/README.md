# Manifest Hydration

To hydrate the manifests in this repository, run the following commands:

```shell
git clone https://github.com/platform-engineer-lab/sample-service-config
# cd into the cloned directory
git checkout 1f22fa1ef686e3250cf3c5ce55d0a23cde3936fa
helm template . --name-template sample-service --namespace sample-service --values ./chart/env/prod/values.yaml --include-crds
```
