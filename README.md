# Kargo Deployment Example

Just an example, if you're not well versed in Argo CD and/or Kustomize, you WILL get lost.

## Deploy

```shell
until kustomize build --enable-helm https://github.com/christianh814/kargo-deployment-example/bootstrap | kubectl apply -f  - ; do sleep 3; done
```


## External Secret 

The following won't work for you unless you export the right stuff. This HAS to be done RIGHT AFTER YOU DEPLOY ^

```shell
kubectl apply -f - <<EOF
apiVersion: external-secrets.io/v1beta1
kind: ClusterSecretStore
metadata:
  name: kargo-demo-repo-css
spec:
  provider:
    fake:
      data:
      - key: "/data/password"
        value: "${KARGO_GH_PAT}"
        version: "v1"
      - key: "/data/username"
        value: "${KARGO_GH_USERNAME}"
        version: "v1"
      - key: "/data/repoURL"
        value: "https://github.com/christianh814/kargo-simple-demo"
        version: "v1"
EOF
```
