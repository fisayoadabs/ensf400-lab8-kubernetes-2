# Assignment 3 - Kubernetes

## Deployment Steps and Outputs

0. Start with these commands

```bash
$ minikube start
😄  minikube v1.32.0 on Ubuntu 20.04 (docker/amd64)
✨  Automatically selected the docker driver. Other choices: none, ssh
📌  Using Docker driver with root privileges
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
💾  Downloading Kubernetes v1.28.3 preload ...
    > preloaded-images-k8s-v18-v1...:  403.35 MiB / 403.35 MiB  100.00% 156.76 
    > gcr.io/k8s-minikube/kicbase...:  453.64 MiB / 453.90 MiB  99.94% 101.18 M
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...
🐳  Preparing Kubernetes v1.28.3 on Docker 24.0.7 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring bridge CNI (Container Networking Interface) ...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🔎  Verifying Kubernetes components...
🌟  Enabled addons: default-storageclass, storage-provisioner
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```
```bash
$ minikube addons enable ingress
```

1. Create a **nginx-configmap.yaml**: Defines a ConfigMap for nginx configuration.
```bash
$ kubectl apply -f nginx-configmap.yaml
configmap/nginx-configmap created
```

2. Create a **nginx-dep.yaml**: Defines a Deployment for nginx with 5 replicas, using nginx version 1.14.2, exposing port 80. It mounts a ConfigMap for configuration.

```bash 
$ kubectl apply -f nginx-dep.yaml
deployment.apps/nginx-dep created
```

3. Create a **nginx-svc.yaml**: Defines a Service for nginx with ClusterIP type, exposing port 80.
```bash
$ kubectl apply -f nginx-svc.yaml
service/nginx-svc created
```

4. Create a **nginx-ingress.yaml**: Defines an Ingress for nginx, redirecting requests to path / to the backend service nginx-svc.
```bash
$ kubectl apply -f nginx-ingress.yaml
ingress.networking.k8s.io/nginx-ingress created
```

5. Create a **app-1-dep.yaml** file and deploy it
```bash
$ kubectl apply -f app-1-dep.yaml
deployment.apps/app-1-dep created
```

6. Create a **app-1-svc.yaml** file and deply it
```bash
$ kubectl apply -f app-1-svc.yaml
service/app-1-svc created
```

7. Create a **app-2-dep.yaml** file and deploy it
```bash
$ kubectl apply -f app-2-dep.yaml
deployment.apps/app-2-dep created
```

8. Create a **app-2-svc.yaml** file and deploy it
```bash
$ kubectl apply -f app-2-svc.yaml
service/app-2-svc created
```

9. Create an **app-1-ingress.yaml** file and deploy it
```bash
$ kubectl apply -f app-1-ingress.yaml
ingress.networking.k8s.io/app-1-ingress created
```

10. Create an **app-2-ingree.yaml** file and deploy it
```bash
$ kubectl apply -f app-2-ingress.yaml
ingress.networking.k8s.io/app-2-ingress created
```

11. Verify that each one of the deployments are running along with the services and ingresses
```bash
$ kubectl get deployments
NAME        READY   UP-TO-DATE   AVAILABLE   AGE
app-1-dep   3/3     3            3           2m6s
app-2-dep   2/2     2            2           106s
nginx-dep   0/5     5            0           2m44s

$ kubectl get services
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
app-1-svc    ClusterIP   10.100.10.177    <none>        80/TCP    2m22s
app-2-svc    ClusterIP   10.109.204.31    <none>        80/TCP    119s
kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP   7m22s
nginx-svc    ClusterIP   10.105.235.174   <none>        80/TCP    2m48s

$ kubectl get ingresses
NAME            CLASS   HOSTS   ADDRESS        PORTS   AGE
app-1-ingress   nginx   *       192.168.49.2   80      68s
app-2-ingress   nginx   *       192.168.49.2   80      58s
nginx-ingress   nginx   *       192.168.49.2   80      3m4s
```

12. Run the curl command
```bash
$ curl http://$(minikube ip)/
Hello World from [app-1-dep-86f67f4f87-2d28z]!
$ curl http://$(minikube ip)/
Hello World from [app-2-dep-7f686c4d8d-lr95c]!

```