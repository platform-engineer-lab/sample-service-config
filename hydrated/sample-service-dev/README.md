# Manifest Hydration

To hydrate the manifests in this repository, run the following commands:

```shell
git clone https://github.com/platform-engineer-lab/sample-service-config
# cd into the cloned directory
git checkout 065bc50cb5b67f40b5bb922b579ae46b91683335
helm template . --name-template sample-service --namespace sample-service --values ./chart/env/dev/values.yaml --include-crds
```
