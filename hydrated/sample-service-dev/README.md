# Manifest Hydration

To hydrate the manifests in this repository, run the following commands:

```shell
git clone https://github.com/platform-engineer-lab/sample-service-config
# cd into the cloned directory
git checkout 0e6a1f050b48bd51281210714b08ee8e36dd4a1d
helm template . --name-template sample-service --namespace business-apps --values ./chart/env/dev/values.yaml --include-crds
```
