# Using the API from the Command Line

we can use `kubectl` and `curl` to demonstrate the use of the Kubernetes API.

```bash
kubectl -n kube-system get deploy/coredns -o=yaml
kubectl api-resources
kubectl api-versions
```

to expose Kubernetes API to local machine

```bash
kubectl proxy --port=8080
```

to receive JSON payloads

```
curl http://127.0.0.1:8080/apis/batch/v1
$ curl http://127.0.0.1:8080/apis/batch/v1beta1
```
