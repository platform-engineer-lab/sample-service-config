# Manifest Hydration

To hydrate the manifests in this repository, run the following commands:

```shell
git clone https://github.com/platform-engineer-lab/sample-service-config
# cd into the cloned directory
git checkout 63a9ffb13888cf500c23072b12eec7047d1c0adc
helm template . --name-template sample-service --namespace sample-service --values ./chart/env/prod/values.yaml --include-crds
```
