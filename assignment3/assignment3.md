# ENSF 400 Assignment 3 - Kubernetes
***
* **Full Name** = Oluwafisayo Adabs
* **UCID** = 30141541
***
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
    > preloaded-images-k8s-v18-v1...:  8.19 MiB / 403.35 MiB [>_] 2.03%    > preloaded-images-k8s-v18-v1...:  37.35 MiB / 403.35 MiB [>] 9.26%    > gcr.io/k8s-minikube/kicbase...:  1.62 KiB / 453.90 MiB [>_] 0.00%    > preloaded-images-k8s-v18-v1...:  59.19 MiB / 403.35 MiB [] 14.67%    > gcr.io/k8s-minikube/kicbase...:  1.64 MiB / 453.90 MiB [>_] 0.36%    > preloaded-images-k8s-v18-v1...:  81.06 MiB / 403.35 MiB  20.10% 1    > preloaded-images-k8s-v18-v1...:  115.09 MiB / 403.35 MiB  28.53%     > gcr.io/k8s-minikube/kicbase...:  23.53 MiB / 453.90 MiB [>] 5.18%    > preloaded-images-k8s-v18-v1...:  146.17 MiB / 403.35 MiB  36.24%     > gcr.io/k8s-minikube/kicbase...:  48.00 MiB / 453.90 MiB  10.58% 7    > preloaded-images-k8s-v18-v1...:  176.30 MiB / 403.35 MiB  43.71%     > gcr.io/k8s-minikube/kicbase...:  51.70 MiB / 453.90 MiB  11.39% 7    > gcr.io/k8s-minikube/kicbase...:  70.34 MiB / 453.90 MiB  15.50% 7    > preloaded-images-k8s-v18-v1...:  210.05 MiB / 403.35 MiB  52.08%     > preloaded-images-k8s-v18-v1...:  232.12 MiB / 403.35 MiB  57.55%     > gcr.io/k8s-minikube/kicbase...:  78.50 MiB / 453.90 MiB  17.29% 7    > gcr.io/k8s-minikube/kicbase...:  88.18 MiB / 453.90 MiB  19.43% 7    > preloaded-images-k8s-v18-v1...:  258.36 MiB / 403.35 MiB  64.05%     > preloaded-images-k8s-v18-v1...:  292.42 MiB / 403.35 MiB  72.50%     > gcr.io/k8s-minikube/kicbase...:  106.34 MiB / 453.90 MiB  23.43%     > gcr.io/k8s-minikube/kicbase...:  115.07 MiB / 453.90 MiB  25.35%     > preloaded-images-k8s-v18-v1...:  322.48 MiB / 403.35 MiB  79.95%     > gcr.io/k8s-minikube/kicbase...:  137.68 MiB / 453.90 MiB  30.33%     > preloaded-images-k8s-v18-v1...:  349.36 MiB / 403.35 MiB  86.61%     > gcr.io/k8s-minikube/kicbase...:  152.24 MiB / 453.90 MiB  33.54%     > preloaded-images-k8s-v18-v1...:  384.87 MiB / 403.35 MiB  95.42%     > preloaded-images-k8s-v18-v1...:  403.35 MiB / 403.35 MiB  100.00% 148.23 
    > gcr.io/k8s-minikube/kicbase...:  168.00 MiB / 453.90 MiB  37.01%     > gcr.io/k8s-minikube/kicbase...:  173.61 MiB / 453.90 MiB  38.25%     > gcr.io/k8s-minikube/kicbase...:  187.98 MiB / 453.90 MiB  41.41%     > gcr.io/k8s-minikube/kicbase...:  192.00 MiB / 453.90 MiB  42.30%     > gcr.io/k8s-minikube/kicbase...:  202.56 MiB / 453.90 MiB  44.63%     > gcr.io/k8s-minikube/kicbase...:  219.21 MiB / 453.90 MiB  48.30%     > gcr.io/k8s-minikube/kicbase...:  235.34 MiB / 453.90 MiB  51.85%     > gcr.io/k8s-minikube/kicbase...:  254.50 MiB / 453.90 MiB  56.07%     > gcr.io/k8s-minikube/kicbase...:  275.66 MiB / 453.90 MiB  60.73%     > gcr.io/k8s-minikube/kicbase...:  303.05 MiB / 453.90 MiB  66.77%     > gcr.io/k8s-minikube/kicbase...:  315.81 MiB / 453.90 MiB  69.58%     > gcr.io/k8s-minikube/kicbase...:  329.60 MiB / 453.90 MiB  72.62%     > gcr.io/k8s-minikube/kicbase...:  346.29 MiB / 453.90 MiB  76.29%     > gcr.io/k8s-minikube/kicbase...:  364.39 MiB / 453.90 MiB  80.28%     > gcr.io/k8s-minikube/kicbase...:  388.61 MiB / 453.90 MiB  85.62%     > gcr.io/k8s-minikube/kicbase...:  407.12 MiB / 453.90 MiB  89.69%     > gcr.io/k8s-minikube/kicbase...:  424.82 MiB / 453.90 MiB  93.59%     > gcr.io/k8s-minikube/kicbase...:  448.00 MiB / 453.90 MiB  98.70%     > gcr.io/k8s-minikube/kicbase...:  453.90 MiB / 453.90 MiB  100.00% 76.60 M
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
💡  ingress is an addon maintained by Kubernetes. For any concerns contact minikube on GitHub.
You can view the list of minikube maintainers at: https://github.com/kubernetes/minikube/blob/master/OWNERS
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20231011-8b53cabe0
    ▪ Using image registry.k8s.io/ingress-nginx/controller:v1.9.4
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20231011-8b53cabe0
🔎  Verifying ingress addon...
🌟  The 'ingress' addon is enabled
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