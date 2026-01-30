# 一、基础环境

![PixPin_2026-01-31_00-59-24](./assets/PixPin_2026-01-31_00-59-24.jpg)

# 二、官方仓库

```http
https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.14.0/deploy/static/provider/baremetal/deploy.yaml
```

# 三、镜像修改

![image-20260131010413635](./assets/image-20260131010413635.png)

![image-20260131010420240](./assets/image-20260131010420240.png)

![image-20260131010424799](./assets/image-20260131010424799.png)



```sh
docker pull registry.k8s.io/ingress-nginx/controller:v1.14.0
```

```sh
docker pull registry.k8s.io/ingress-nginx/kube-webhook-certgen:v1.6.4
```

```sh
docker tag registry.k8s.io/ingress-nginx/controller:v1.14.0 shixiaochuangk8s/ingress-nginx-controller:v1.14.0
```

```sh
docker tag registry.k8s.io/ingress-nginx/kube-webhook-certgen:v1.6.4 shixiaochuangk8s/ingress-nginx-kube-webhook-certgen:v1.6.4
```

```sh
docker push shixiaochuangk8s/ingress-nginx-controller:v1.14.0
```

```sh
docker push shixiaochuangk8s/ingress-nginx-kube-webhook-certgen:v1.6.4
```

# 四、部署

外部的负载均衡器为metallb：

![image-20260131011649325](./assets/image-20260131011649325.png)

```sh
kubectl apply -f deploy-metallb.yaml
```

```sh
kubectl get pods -n ingress-nginx
```

![image-20260131011245616](./assets/image-20260131011245616.png)

外部的负载均衡器为openelb：

![image-20260131011102295](./assets/image-20260131011102295.png)

![image-20260131011108844](./assets/image-20260131011108844.png)

```yaml
annotations:
    lb.kubesphere.io/v1alpha1: openelb
    protocol.openelb.kubesphere.io/v1alpha1: layer2
    eip.openelb.kubesphere.io/v1alpha2: eip-pool
```

```sh
kubectl apply -f deploy-openelb.yaml
```

![image-20260131011441857](./assets/image-20260131011441857.png)