## k8s

### pod

pods have any number containers, and it can have it's own privete IP and hostname. 

### ReplicationController

It make sure that there is always a running pod instance.

It create the pod.

### service

Because the exist of pod is short-lived(e.g. node failure or be deleted), so the ReplicationController will replace the miss pod to new pod. But the IP between old and new pod is different, now we need service(IP is static).


