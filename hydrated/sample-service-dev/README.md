# Manifest Hydration

To hydrate the manifests in this repository, run the following commands:

```shell
git clone https://github.com/platform-engineer-lab/sample-service-config
# cd into the cloned directory
git checkout 1430bd072dd2c6d73566f3bd1630237561b2ae5b
helm template . --name-template sample-service --namespace sample-service --values ./chart/env/dev/values.yaml --include-crds
```
