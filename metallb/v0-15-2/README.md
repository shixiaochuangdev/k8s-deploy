# 一、基础环境

![PixPin_2026-01-31_00-44-23](./assets/PixPin_2026-01-31_00-44-23.jpg)

# 二、官方仓库

```http
https://raw.githubusercontent.com/metallb/metallb/v0.15.2/config/manifests/metallb-native.yaml
```

# 三、镜像修改

![image-20260131004614540](./assets/image-20260131004614540.png)

![image-20260131004621971](./assets/image-20260131004621971.png)



```sh
docker pull quay.io/metallb/controller:v0.15.2
```

```sh
docker pull quay.io/metallb/speaker:v0.15.2
```

```sh
docker tag quay.io/metallb/speaker:v0.15.2 shixiaochuangk8s/metallb-speaker:v0.15.2
```

```sh
docker tag quay.io/metallb/controller:v0.15.2 shixiaochuangk8s/metallb-controller:v0.15.2
```

```sh
docker push shixiaochuangk8s/metallb-speaker:v0.15.2
```

```sh
docker push shixiaochuangk8s/metallb-controller:v0.15.2
```

# 四、部署

```http
https://metallb.universe.tf/installation/
```

![image-20260131004647410](./assets/image-20260131004647410.png)

```sh
kubectl edit configmap -n kube-system kube-proxy
```

![PixPin_2026-01-31_00-47-50](./assets/PixPin_2026-01-31_00-47-50.jpg)

```sh
kubectl apply -f metallb-native.yaml
```

```sh
kubectl get all -n metallb-system
```

![PixPin_2026-01-31_00-51-57](./assets/PixPin_2026-01-31_00-51-57.jpg)

```sh
kubectl apply -f ip-pool.yaml
```

```sh
kubectl get ipaddresspool -n metallb-system
```

![PixPin_2026-01-31_00-52-41](./assets/PixPin_2026-01-31_00-52-41.jpg)







