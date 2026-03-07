# 一、基础环境

![PixPin_2026-03-07_20-49-29](./assets/PixPin_2026-03-07_20-49-29.jpg)

# 二、部署

```sh
kubectl create namespace gateway-api
```

```sh
kubectl apply --server-side -f standard-install.yaml
```

```sh
kubectl apply -f kubernetes-crd-rbac.yml
```

```sh
kubectl apply -f traefik-config.yaml
```

```sh
kubectl apply -f traefik-deploy.yaml
```

```sh
kubectl get pods -n gateway-api
```

![PixPin_2026-03-07_20-40-01](./assets/PixPin_2026-03-07_20-40-01.jpg)

```sh
kubectl apply -f traefik-service.yaml
```

```sh
kubectl apply -f traefik-gatewayClass.yaml
```

```sh
kubectl apply -f traefik-gateway.yaml
```

```sh
kubectl get gateway -n gateway-api
```

![PixPin_2026-03-07_20-43-07](./assets/PixPin_2026-03-07_20-43-07.jpg)

```sh
kubectl apply -f traefik-dashboard.yaml
```



