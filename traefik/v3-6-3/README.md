# 一、基础环境说明

![PixPin_2026-01-23_18-37-45](./assets/PixPin_2026-01-23_18-37-45.jpg)

# 二、官方仓库

```http
https://github.com/traefik/traefik/blob/v3.6.3/docs/content/reference/dynamic-configuration/kubernetes-crd-definition-v1.yml
```

```http
https://github.com/traefik/traefik/blob/v3.6.3/docs/content/reference/dynamic-configuration/kubernetes-crd-rbac.yml
```

```http
https://raw.githubusercontent.com/openelb/openelb/refs/tags/v0.6.0/deploy/openelb.yaml
```

# 三、部署

```sh
kubectl apply -f kubernetes-crd-definition-v1.yml
```

```sh
kubectl apply -f kubernetes-crd-rbac.yml 
```

```sh
kubectl apply -f traefik-config.yaml
```

```sh
kubectl apply -f openelb.yaml
```

```sh
kubectl get pods -n openelb-system
```

![PixPin_2026-01-23_17-52-13](./assets/PixPin_2026-01-23_17-52-13.jpg)

```yaml
kubectl apply -f eip.yaml
```

```sh
kubectl apply -f traefik-deploy.yaml
```

```sh
kubectl get pods -n traefik
```

![PixPin_2026-01-23_18-33-11](./assets/PixPin_2026-01-23_18-33-11.jpg)

```sh
kubectl apply -f traefik-service.yaml
```

```sh
kubectl apply -f traefik-dashboard.yaml
```

![PixPin_2026-01-23_18-37-21](./assets/PixPin_2026-01-23_18-37-21.jpg)

```http
http://traefikui.shixiaochuang.org/dashboard/
```

![PixPin_2026-01-23_18-36-53](./assets/PixPin_2026-01-23_18-36-53.jpg)

![PixPin_2026-01-23_18-36-41](./assets/PixPin_2026-01-23_18-36-41.jpg)
