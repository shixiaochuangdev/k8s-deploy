# 一、基础环境说明

![PixPin_2026-02-01_16-06-28](./assets/PixPin_2026-02-01_16-06-28.jpg)

# 二、部署

前提：

1、集群中存在动态供给

![PixPin_2026-02-01_16-07-21](./assets/PixPin_2026-02-01_16-07-21.jpg)

2、集群中存在ingress nginx controller

![PixPin_2026-02-01_16-08-02](./assets/PixPin_2026-02-01_16-08-02.jpg)

```sh
kubectl create namespace prometheus-ns
```

```sh
kubectl apply -f prometheus-pvc.yaml
```

```sh
kubectl apply -f prometheus-rbac.yaml
```

```sh
kubectl apply -f prometheus-cfg.yaml
```

```sh
kubectl apply -f prometheus-deploy.yaml
```

```sh
kubectl apply -f prometheus-svc.yaml
```

```sh
kubectl apply -f prometheus-ingress.yaml
```

```sh
kubectl apply -f prometheus-traefik.yaml
```

```http
http://prometheusui.shixiaochuang.org
```

![image-20260201161156624](./assets/image-20260201161156624.png)

```sh
kubectl create namespace grafana-ns
```

```sh
kubectl apply -f grafana-pvc.yaml
```

```sh
kubectl apply -f grafana-datasources-cfg.yaml
```

```sh
kubectl apply -f grafana-admin-secret.yaml
```

```sh
kubectl apply -f grafana-deploy.yaml
```

```sh
kubectl apply -f grafana-svc-ingress.yaml
```

![image-20260201162410378](./assets/image-20260201162410378.png)









