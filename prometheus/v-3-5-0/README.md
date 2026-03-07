# 一、基础环境说明

![PixPin_2026-02-01_16-06-28](./assets/PixPin_2026-02-01_16-06-28.jpg)

# 二、部署

```sh
kubectl create namespace monitor-ns
```

```sh
kubectl apply -f prometheus-pvc.yaml
```

```sh
kubectl apply -f prometheus-rbac.yaml
```

关于配置文件的说明：

```sh
# 默认配置文件
kubectl apply -f prometheus-cfg.yaml
```

```sh
# 包含service的自动发现
kubectl apply -f prometheus-cfg-service.yaml
```

```sh
# 包含kube-state-metrics
kubectl apply -f prometheus-cfg-ksm.yaml
```

```sh
# 包含pods的自动发现
kubectl apply -f prometheus-cfg-pod.yaml
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

```http
http://prometheusui.shixiaochuang.org
```

![image-20260201161156624](./assets/image-20260201161156624.png)

或者：

```sh
kubectl apply -f prometheus-traefik.yaml
```

```http
http://prometheusui.shixiaochuang.net
```

![PixPin_2026-03-07_21-45-07](./assets/PixPin_2026-03-07_21-45-07.jpg)

或者：

```sh
kubectl apply -f prometheus-gatewayapi.yaml
```

```http
http://prometheusui.shixiaochuang.io/query
```

![PixPin_2026-03-07_21-58-22](./assets/PixPin_2026-03-07_21-58-22.jpg)

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

```shell
kubectl apply -f grafana-svc.yaml
```

```sh
kubectl apply -f grafana-ingress.yaml
```

```http
http://grafana.shixiaochuang.org/login
```

![image-20260201162410378](./assets/image-20260201162410378.png)

或者：

```sh
kubectl apply -f grafana-traefik.yaml
```

```http
http://grafana.shixiaochuang.net/login
```

![PixPin_2026-03-07_22-12-57](./assets/PixPin_2026-03-07_22-12-57.jpg)

或者：

```sh
kubectl apply -f grafana-gatewayapi.yaml
```

```http
http://grafana.shixiaochuang.io/login
```

![PixPin_2026-03-07_22-16-21](./assets/PixPin_2026-03-07_22-16-21.jpg)





