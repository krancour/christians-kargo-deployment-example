# Kargo Deployment Example

Just an example, if you're not well versed in Argo CD and/or Kustomize, you WILL get lost.

## Deploy

```shell
until kustomize build --enable-helm https://github.com/christianh814/kargo-deployment-example/bootstrap | kubectl apply -f  - ; do sleep 3; done
```


## Patch

Patch or it won't work. A Dummy secret is stored here just for example purposes. You don't need this patch if you've replaced the example secret with something like an https://external-secrets.io/ object.

```shell
kubectl patch secrets -n kargo-demo kargo-demo-repo -p "{\"stringData\":{\"password\":\"${KARGO_GH_PAT}\"}}"
```
