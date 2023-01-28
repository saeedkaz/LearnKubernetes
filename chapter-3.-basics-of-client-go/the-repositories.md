# The Repositories

## The Client Library

Kubernetes programming interface in Go mainly consists of the client-go library.

Cleint-go is the typical web service client library that supports all official parts of Kubernetes.

It can be used to execute usual REST verbs:&#x20;

* Create
* Get
* List
* Update
* Delete
* Patch

It also supports the verb Watch which is special for Kubernetes-like APIs.&#x20;

The most important packages are

* tools/clientcmd: To setup client from kubeconfig file
* kubernetes/: actual Kubernetes API Clients

## Kubernetes API Types

The Kubernetes API Go types for objects like pods, services, and deployments are located in [their own repository](http://bit.ly/2ZA6dWH). It is accessed as `k8s.io/api` in Go code.

## API Machinery

It includes all the generic building blocks to implement a Kubernetes-like API.&#x20;

API Machinery is not restricted to container management, so, for example, it could be used to build APIs for an online shop or any other business-specific domain.

An important one is _k8s.io/apimachinery/pkg/apis/meta/v1._ It contains many of the generic API types such as `ObjectMeta`, `TypeMeta`, `GetOptions`, and `ListOptions`

## Creating and Using a Client

```go
import (
    metav1 "k8s.io/apimachinery/pkg/apis/meta/v1"
    "k8s.io/client-go/tools/clientcmd"
    "k8s.io/client-go/kubernetes"
)

kubeconfig = flag.String("kubeconfig", "~/.kube/config", "kubeconfig file")
flag.Parse()
config, err := clientcmd.BuildConfigFromFlags("", *kubeconfig)
clientset, err := kubernetes.NewForConfig(config)

pod, err := clientset.CoreV1().Pods("book").Get("example", metav1.GetOptions{})
```

When running a binary inside of a pod in a cluster, the `kubelet` will automatically mount a service account into the container at _/var/run/secrets/kubernetes.io/serviceaccount_.

```go
config, err := rest.InClusterConfig()
if err != nil {
    // fallback to kubeconfig
    kubeconfig := filepath.Join("~", ".kube", "config")
    if envvar := os.Getenv("KUBECONFIG"); len(envvar) >0 {
        kubeconfig = envvar
    }
    config, err = clientcmd.BuildConfigFromFlags("", kubeconfig)
    if err != nil {
        fmt.Printf("The kubeconfig cannot be loaded: %v\n", err
        os.Exit(1)
    }
}
```

## Versioning and Compatibility

### client side:&#x20;

v1, v1beta2, and v1beta1

### client-go compatibility with Kubernetes versions

Three is an official support matrix

## API Versions and Compatibility Guarantees

alpha, beta, and GA (general availability)

* _alpha versions:_ `v1alpha1`, `v1alpha2`, `v2alpha1`
* _beta versions:_ `v1beta1`, `v1beta2`, `v2beta1`
* table, generally available APIs: `v1`, `v2`
