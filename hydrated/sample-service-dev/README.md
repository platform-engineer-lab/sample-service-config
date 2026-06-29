# Manifest Hydration

To hydrate the manifests in this repository, run the following commands:

```shell
git clone https://github.com/platform-engineer-lab/sample-service-config
# cd into the cloned directory
git checkout fadde74c4556924df6ca2b7bc74275fbda2a6d19
helm template . --name-template sample-service --namespace sample-service --values ./chart/env/dev/values.yaml --include-crds
```
