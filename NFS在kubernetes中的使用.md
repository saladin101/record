## 安装nfs

本次测试使用master节点作为nfs server，其他两台node作为nfs客户端。在所有三台机器上都安装nfs。

**# yum -y install nfs-utils**

## NFS server配置共享目录

- 创建共享目录

**# mkdir -p /home/ps**

- 设置目录访问权限

**# chmod -R 777 /home/ps**

- 设置目录共享文件

**# vi /etc/exports**

```
/home/ps *(rw,no_root_squash,sync)
```

- 使配置生效

**# exportfs -r**

- 查看共享目录

**# exportfs**

`/home/ps	<world>`

- 重启rpcbind服务和nfs服务


**# systemctl restart rpcbind && systemctl enable rpcbind**


**# systemctl restart nfs && systemctl enable nfs**


**# showmount -e 192.168.205.90**

```
Export list for 192.168.205.90:
/home/ps *
```
- 新建两个测试用的目录

**# mkdir -p /home/ps/pv01**

**# mkdir -p /home/ps/pv02**
- 同样将这两个目录添加到nfs共享目录中

**# vi /etc/exports**
```
/home/ps *(rw,no_root_squash,sync)
/home/ps/pv01 *(rw,no_root_squash,sync)
/home/ps/pv02 *(rw,no_root_squash,sync)
```
- 重启服务

**# systemctl restart rpcbind && systemctl restart nfs**
- 查看共享目录信息

**# showmount -e 192.168.205.90**
```
Export list for 192.168.205.90:
/home/ps/pv02 *
/home/ps/pv01 *
/home/ps      *
```
- 创建持久卷

**# vi nfs-pv01.yaml**
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nfs-pv01
  labels:
    pv: nfs-pv01
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Recycle
  storageClassName: nfs
  nfs:
    path: /home/ps/pv01
    server: 192.168.205.90
```
**# vi nfs-pv02.yaml**
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nfs-pv02
  labels:
    pv: nfs-pv02
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Recycle
  storageClassName: nfs
  nfs:
    path: /home/ps/pv02
    server: 192.168.205.90
```
- 启动持久卷

**# kubectl apply -f nfs-pv01.yaml**

**# kubectl apply -f nfs-pv02.yaml**
- 查看持久卷信息

**# kubectl get pv**
```
NAME       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   REASON   AGE
nfs-pv01   1Gi        RWO            Recycle          Available           nfs                     13s
nfs-pv02   1Gi        RWO            Recycle          Available           nfs                     8s
```
- 创建pvc

**# vi nfs-pvc01.yaml**
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nfs-pvc01
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  storageClassName: nfs
  selector:
    matchLabels:
      pv: nfs-pv01
```
**# vi nfs-pvc02.yaml**
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nfs-pvc02
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  storageClassName: nfs
  selector:
    matchLabels:
      pv: nfs-pv02
```
- 启动pvc

**# kubectl apply -f nfs-pvc01.yaml**

**# kubectl apply -f nfs-pvc02.yaml**
- 查看pvc信息

**# kubectl get pvc**
```
NAME        STATUS   VOLUME     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
nfs-pvc01   Bound    nfs-pv01   1Gi        RWO            nfs            10s
nfs-pvc02   Bound    nfs-pv02   1Gi        RWO            nfs            7s
```
- 创建测试用pod配置文件

**# vi nfs-pod01.yaml**
```
kind: Pod
apiVersion: v1
metadata:
  name: nfs-pod01
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: nfs-pv01
  volumes:
    - name: nfs-pv01
      persistentVolumeClaim:
        claimName: nfs-pvc01
```
**# vi nfs-pod02.yaml**
```
kind: Pod
apiVersion: v1
metadata:
  name: nfs-pod02
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: nfs-pv02
  volumes:
    - name: nfs-pv02
      persistentVolumeClaim:
        claimName: nfs-pvc02
```
- 创建pod

**# kubectl apply -f nfs-pod01.yaml**

**# kubectl apply -f nfs-pod02.yaml**
- 查看pod状态

**# kubectl get pod**
```
NAME        READY   STATUS    RESTARTS   AGE
nfs-pod01   1/1     Running   0          2m35s
nfs-pod02   1/1     Running   0          2m32s
```
**# kubectl exec nfs-pod01 touch /var/www/html/index001.html**

**# kubectl exec nfs-pod02 touch /var/www/html/index002.html**
```
**# ls /home/ps/pv01**
index001.html
**# ls /home/ps/pv02**
index002.html
```
**# kubectl exec -it nfs-pod01 /bin/bash**
```
root@nfs-pod01:/# df -h
Filesystem                    Size  Used Avail Use% Mounted on
overlay                        10G  2.9G  7.2G  29% /
tmpfs                          64M     0   64M   0% /dev
tmpfs                         481M     0  481M   0% /sys/fs/cgroup
/dev/mapper/centos-root        10G  2.9G  7.2G  29% /etc/hosts
shm                            64M     0   64M   0% /dev/shm
192.168.205.90:/home/ps/pv01   31G   33M   31G   1% /var/www/html
tmpfs                         481M   12K  481M   1% /run/secrets/kubernetes.io/serviceaccount
tmpfs                         481M     0  481M   0% /proc/acpi
tmpfs                         481M     0  481M   0% /proc/scsi
tmpfs                         481M     0  481M   0% /sys/firmware
root@nfs-pod01:/# ls /var/www/html
index001.html
```

**# kubectl delete -f nfs-pod01.yaml**

**# kubectl get pv**
```
NAME       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM               STORAGECLASS   REASON   AGE
nfs-pv01   1Gi        RWO            Recycle          Bound    default/nfs-pvc01   nfs                     15m
nfs-pv02   1Gi        RWO            Recycle          Bound    default/nfs-pvc02   nfs                     15m
```
**# kubectl get pvc**
```
NAME        STATUS   VOLUME     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
nfs-pvc01   Bound    nfs-pv01   1Gi        RWO            nfs            10m
nfs-pvc02   Bound    nfs-pv02   1Gi        RWO            nfs            10m
```
**# ls /home/ps/pv01**
`index001.html`

**# kubectl delete -f nfs-pvc01.yaml**

**# kubectl get pv**
```
NAME       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM               STORAGECLASS   REASON   AGE
nfs-pv01   1Gi        RWO            Recycle          Available                       nfs                     17m
nfs-pv02   1Gi        RWO            Recycle          Bound       default/nfs-pvc02   nfs                     17m
```
**# kubectl get pvc**
```
NAME        STATUS   VOLUME     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
nfs-pvc02   Bound    nfs-pv02   1Gi        RWO            nfs            11m
```
**# ls /home/ps/pv01**
**# **
