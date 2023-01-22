# Resource

A set of HTTP endpoints (paths) exposing the CRUD (create, read, update, delete) semantics of a certain object type in the system. Common paths are:

* The root, such as _…/pods_, which lists all instances of that type
* A path for individual named resources, such as _…/pods/nginx_

## _subresources_&#x20;

* Resources that have further endpoints to perform specific actions (e.g., …/pod/nginx/port-forward, …/pod/nginx/exec, or …/pod/nginx/logs).
* Usually implement custom protocols instead of REST

## **TIP**

Resources and kinds are often mixed up. Note the clear distinction:

* Resources correspond to HTTP paths.
* Kinds are the types of objects returned by and received by these endpoints, as well as persisted into `etcd`

## GVR

