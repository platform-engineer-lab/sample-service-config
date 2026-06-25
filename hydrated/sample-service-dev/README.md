# Manifest Hydration

To hydrate the manifests in this repository, run the following commands:

```shell
git clone https://github.com/platform-engineer-lab/sample-service-config
# cd into the cloned directory
git checkout 10e3ae67e05ece2485e1e464b130aaae8ea565ef
helm template . --name-template sample-service --namespace sample-service --values ./chart/env/dev/values.yaml --include-crds
```
