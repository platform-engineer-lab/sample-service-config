# Manifest Hydration

To hydrate the manifests in this repository, run the following commands:

```shell
git clone https://github.com/platform-engineer-lab/sample-service-config
# cd into the cloned directory
git checkout 149101447c11673a9afbbc021a6fa6f134d2352f
helm template . --name-template sample-service --namespace business-apps --values ./chart/env/dev/values.yaml --include-crds
```
