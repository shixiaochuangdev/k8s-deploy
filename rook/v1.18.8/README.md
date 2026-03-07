# 一、基础环境

![PixPin_2026-03-07_16-56-48](./assets/PixPin_2026-03-07_16-56-48.jpg)

![image-20260307175030296](./assets/image-20260307175030296.png)

# 二、镜像修改

```http
https://raw.githubusercontent.com/rook/rook/refs/tags/v1.18.8/deploy/examples/csi-operator.yaml
```

![PixPin_2026-03-07_16-58-42](./assets/PixPin_2026-03-07_16-58-42.jpg)

```sh
docker pull quay.io/cephcsi/ceph-csi-operator:v0.4.1
```

```sh
docker tag quay.io/cephcsi/ceph-csi-operator:v0.4.1 shixiaochuangk8s/cephcsi-ceph-csi-operator:v0.4.1
```

```sh
docker push shixiaochuangk8s/cephcsi-ceph-csi-operator:v0.4.1
```

```http
github.com/rook/rook/raw/refs/tags/v1.18.8/deploy/examples/operator.yaml
```

![PixPin_2026-03-07_17-08-31](./assets/PixPin_2026-03-07_17-08-31.jpg)

```sh
docker pull docker.io/rook/ceph:v1.18.8
```

```sh
docker tag docker.io/rook/ceph:v1.18.8  shixiaochuangk8s/rook-ceph:v1.18.8
```

```sh
docker pull shixiaochuangk8s/rook-ceph:v1.18.8
```

```http
https://raw.githubusercontent.com/rook/rook/refs/tags/v1.18.8/deploy/examples/cluster.yaml
```

![PixPin_2026-03-07_17-17-39](./assets/PixPin_2026-03-07_17-17-39.jpg)

```http
https://raw.githubusercontent.com/rook/rook/refs/tags/v1.18.8/deploy/examples/toolbox.yaml
```

![PixPin_2026-03-07_17-26-40](./assets/PixPin_2026-03-07_17-26-40.jpg)

```sh
docker pull quay.io/ceph/ceph:v19.2.3
```

```sh
docker tag quay.io/ceph/ceph:v19.2.3 shixiaochuangk8s/ceph-ceph:v19.2.3
```

```sh
docker push shixiaochuangk8s/ceph-ceph:v19.2.3
```

# 三、部署

```sh
kubectl apply -f crds.yaml
```

```sh
kubectl apply -f common.yaml
```

```sh
kubectl apply -f csi-operator.yaml
```

```sh
kubectl get pods -l control-plane=ceph-csi-op-controller-manager -n rook-ceph
```

![PixPin_2026-03-07_17-05-54](./assets/PixPin_2026-03-07_17-05-54.jpg)

```shell
kubectl apply -f operator.yaml
```

```sh
kubectl get pods -n rook-ceph -l app=rook-ceph-operator
```

![PixPin_2026-03-07_17-15-16](./assets/PixPin_2026-03-07_17-15-16.jpg)

```sh
kubectl apply -f cluster.yaml
```

```sh
kubectl get pods -n rook-ceph
```

![PixPin_2026-03-07_17-36-37](./assets/PixPin_2026-03-07_17-36-37.jpg)

```sh
kubectl apply -f toolbox.yaml
```

```sh
kubectl get pods -n rook-ceph -l app=rook-ceph-tools
```

![PixPin_2026-03-07_17-38-00](./assets/PixPin_2026-03-07_17-38-00.jpg)

```sh
kubectl -n rook-ceph exec -it deploy/rook-ceph-tools -- bash
```

```sh
ceph status
```

![PixPin_2026-03-07_17-38-27](./assets/PixPin_2026-03-07_17-38-27.jpg)

```sh
vim ~/.bashrc
```

在文件末尾追加

```sh
# === Rook Ceph 常用快捷命令 ===
cephsh() {
  kubectl -n rook-ceph exec -it deploy/rook-ceph-tools -- bash
}
```

```sh
source ~/.bashrc
```

```sh
kubectl apply -f rook-ceph-mgr-dashboard.yaml
```

```http
https://192.168.200.157:30443/
```

```sh
kubectl -n rook-ceph get secret rook-ceph-dashboard-password -o jsonpath="{['data']['password']}" | base64 -d
```

![PixPin_2026-03-07_17-41-02](./assets/PixPin_2026-03-07_17-41-02.jpg)

![PixPin_2026-03-07_17-40-50](./assets/PixPin_2026-03-07_17-40-50.jpg)

![PixPin_2026-03-07_17-44-00](./assets/PixPin_2026-03-07_17-44-00.jpg)

后续如果要用到cephfs需要部署：

```sh
kubectl apply -f filesystem.yaml
```

后续如果要用到object需要部署：

```sh
kubectl apply -f object.yaml
```

```sh
kubectl apply -f object-user.yaml
```

```sh
kubectl get secret rook-ceph-object-user-my-store-my-user \
-n rook-ceph \
-o jsonpath='{.data.AccessKey}' | base64 -d
```

```sh
kubectl get secret rook-ceph-object-user-my-store-my-user \
-n rook-ceph \
-o jsonpath='{.data.SecretKey}' | base64 -d
```

```sh
kubectl apply -f rgw-ingress.yaml
```

后续使用s3客户端测试即可！！
