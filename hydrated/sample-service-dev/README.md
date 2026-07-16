# Manifest Hydration

To hydrate the manifests in this repository, run the following commands:

```shell
git clone https://github.com/platform-engineer-lab/sample-service-config
# cd into the cloned directory
git checkout 9dacce1a8846a92085bc3357de34fe107ec5afb1
helm template . --name-template sample-service --namespace business-apps --values ./chart/env/dev/values.yaml --include-crds
```
