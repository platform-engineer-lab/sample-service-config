# Manifest Hydration

To hydrate the manifests in this repository, run the following commands:

```shell
git clone https://github.com/platform-engineer-lab/sample-service-config
# cd into the cloned directory
git checkout 41fc6364eaa34970b490d7238924514b64b126f9
helm template . --name-template sample-service --namespace business-apps --values ./chart/env/dev/values.yaml --include-crds
```
