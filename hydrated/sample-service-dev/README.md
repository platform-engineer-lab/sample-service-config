# Manifest Hydration

To hydrate the manifests in this repository, run the following commands:

```shell
git clone https://github.com/platform-engineer-lab/sample-service-config
# cd into the cloned directory
git checkout a64f79717d61149fb53685c2018f4dd358417769
helm template . --name-template sample-service --namespace business-apps --values ./chart/env/dev/values.yaml --include-crds
```
