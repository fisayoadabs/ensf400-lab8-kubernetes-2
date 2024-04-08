# Assignment 3 - Kubernetes

## Deployment Steps and Outputs

```bash
$ minikube start
```
1. Create a **nginx-dep.yaml**: Defines a Deployment for nginx with 5 replicas, using nginx version 1.14.2, exposing port 80. It mounts a ConfigMap for configuration.

```bash 
$ kubectl apply -f nginx-dep.yaml
deployment.apps/nginx-dep created
```

2. Create a **nginx-configmap.yaml**: Defines a ConfigMap for nginx configuration.
```bash
$ kubectl apply -f nginx-configmap.yaml
configmap/nginx-configmap created
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
app-1-dep   3/3     3            3           55m
app-2-dep   2/2     2            2           54m
nginx-dep   0/5     5            0           56m

$ kubectl get services
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
app-1-svc    ClusterIP   10.107.143.193   <none>        8080/TCP   55m
app-2-svc    ClusterIP   10.106.81.79     <none>        8080/TCP   54m
kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP    61m
nginx-svc    ClusterIP   10.108.222.171   <none>        80/TCP     55m

$ kubectl get ingresses
NAME            CLASS    HOSTS   ADDRESS   PORTS   AGE
app-1-ingress   <none>   *                 80      54m
app-2-ingress   <none>   *                 80      54m
nginx-ingress   <none>   *                 80      56m
```

12. Run the curl command
```bash
$ curl http://$(minikube ip)/
Hello World from [app-1-dep-86f67f4f87-2d28z]!
$ curl http://$(minikube ip)/
Hello World from [app-2-dep-7f686c4d8d-lr95c]!

```