# 一、基础环境

ceph集群：

![PixPin_2026-03-07_18-07-01](./assets/PixPin_2026-03-07_18-07-01.jpg)

消费集群：

![PixPin_2026-03-07_18-00-48](./assets/PixPin_2026-03-07_18-00-48.jpg)

# 二、镜像修改

```http
https://raw.githubusercontent.com/ceph/ceph-csi/refs/tags/v3.15.1/deploy/rbd/kubernetes/csi-rbdplugin-provisioner.yaml
```

![PixPin_2026-03-07_18-13-13](./assets/PixPin_2026-03-07_18-13-13.jpg)

```sh
docker pull quay.io/cephcsi/cephcsi:v3.15.1
```

```sh
docker tag quay.io/cephcsi/cephcsi:v3.15.1 shixiaochuangk8s/cephcsi-cephcsi:v3.15.1
```

```sh
docker push shixiaochuangk8s/cephcsi-cephcsi:v3.15.1
```

![PixPin_2026-03-07_18-15-30](./assets/PixPin_2026-03-07_18-15-30.jpg)

```sh
docker pull registry.k8s.io/sig-storage/csi-provisioner:v5.1.0
```

```sh
docker tag registry.k8s.io/sig-storage/csi-provisioner:v5.1.0 shixiaochuangk8s/sig-storage-csi-provisioner:v5.1.0
```

```sh
docker push shixiaochuangk8s/sig-storage-csi-provisioner:v5.1.0
```

![PixPin_2026-03-07_19-11-14](./assets/PixPin_2026-03-07_19-11-14.jpg)

```sh
docker pull registry.k8s.io/sig-storage/csi-snapshotter:v8.2.0
```

```sh
docker tag registry.k8s.io/sig-storage/csi-snapshotter:v8.2.0 shixiaochuangk8s/sig-storage-csi-snapshotter:v8.2.0
```

```sh
docker push shixiaochuangk8s/sig-storage-csi-snapshotter:v8.2.0
```

![PixPin_2026-03-07_19-26-43](./assets/PixPin_2026-03-07_19-26-43.jpg)

```sh
docker pull registry.k8s.io/sig-storage/csi-attacher:v4.8.0
```

```sh
docker tag registry.k8s.io/sig-storage/csi-attacher:v4.8.0 shixiaochuangk8s/sig-storage-csi-attacher:v4.8.0
```

```sh
docker push shixiaochuangk8s/sig-storage-csi-attacher:v4.8.0
```

![PixPin_2026-03-07_19-28-36](./assets/PixPin_2026-03-07_19-28-36.jpg)

```sh
docker pull registry.k8s.io/sig-storage/csi-resizer:v1.13.1
```

```sh
docker tag  registry.k8s.io/sig-storage/csi-resizer:v1.13.1 shixiaochuangk8s/sig-storage-csi-resizer:v1.13.1
```

```sh
docker push shixiaochuangk8s/sig-storage-csi-resizer:v1.13.1
```

```http
https://raw.githubusercontent.com/ceph/ceph-csi/refs/tags/v3.15.1/deploy/rbd/kubernetes/csi-rbdplugin.yaml
```

![PixPin_2026-03-07_19-38-08](./assets/PixPin_2026-03-07_19-38-08.jpg)

```sh
docker pull registry.k8s.io/sig-storage/csi-node-driver-registrar:v2.13.0
```

```sh
docker tag registry.k8s.io/sig-storage/csi-node-driver-registrar:v2.13.0 shixiaochuangk8s/sig-storage-csi-node-driver-registrar:v2.13.0
```

```sh
docker push shixiaochuangk8s/sig-storage-csi-node-driver-registrar:v2.13.0
```

# 三、部署

```sh
kubectl create namespace ceph-csi-rbd
```

```sh
kubectl apply -f csidriver.yaml
```

```sh
kubectl apply -f csi-provisioner-rbac.yaml
```

```sh
kubectl apply -f csi-nodeplugin-rbac.yaml
```

```sh
kubectl apply -f csi-config-map.yaml
```

```sh
kubectl apply -f ceph-conf.yaml
```

```sh
kubectl apply -f csi-rbdplugin-provisioner.yaml
```

```sh
kubectl get pods -l app=csi-rbdplugin-provisioner -n ceph-csi-rbd
```

![PixPin_2026-03-07_19-35-20](./assets/PixPin_2026-03-07_19-35-20.jpg)

```sh
kubectl apply -f csi-rbdplugin.yaml
```

```sh
kubectl get pods -l app=csi-rbdplugin -n ceph-csi-rbd
```

![PixPin_2026-03-07_19-40-32](./assets/PixPin_2026-03-07_19-40-32.jpg)

```sh
kubectl get all -n ceph-csi-rbd
```

![PixPin_2026-03-07_19-40-54](./assets/PixPin_2026-03-07_19-40-54.jpg)

# 四、测试

```sh
# 创建存储池
ceph osd pool create kube-rbddata 16 16
```

```sh
# 启用rbd功能
ceph osd pool application enable kube-rbddata rbd
```

```sh
ceph osd pool application get kube-rbddata
```

```sh
# 存储池初始化
rbd pool init -p kube-rbddata
```

```sh
ceph osd pool stats kube-rbddata
```

![PixPin_2026-03-07_19-42-45](./assets/PixPin_2026-03-07_19-42-45.jpg)

```sh
# 创建专属的账号信息
ceph auth get-or-create client.k8s \
  mon 'allow r' \
  osd 'allow rwx pool=kube-rbddata'
```

```sh
# 查看用户信息确认
ceph auth get client.k8s
```

![PixPin_2026-03-07_19-43-48](./assets/PixPin_2026-03-07_19-43-48.jpg)

```sh
kubectl  apply -f csi-rbd-secret.yaml
```

```sh
kubectl  apply -f csi-rbd-sc.yaml
```

![PixPin_2026-03-07_19-46-32](./assets/PixPin_2026-03-07_19-46-32.jpg)

```sh
kubectl apply -f rbd-pvc.yaml
```

```sh
kubectl get pvc
```

![PixPin_2026-03-07_19-47-49](./assets/PixPin_2026-03-07_19-47-49.jpg)
