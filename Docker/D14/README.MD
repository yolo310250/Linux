## 第十四週上課

**Persistent Volume**

- 安裝NFS Server
```
yum install nfs-utils
mkdir /var/nfsshare
chmod -R 777 /var/nfsshare/
編輯 /etc/exports
加入/var/nfsshare 192.168.56.0(rw,sync,no_root_squash,no_all_squash)

systemctl restart rpcbind
systemctl restart nfs-server
```
- 安裝NFS Client
```
yum install nfs-utils
mkdir -p /mnt/nfs/var/nfsshare
mount -t nfs 192.168.56.117:/var/nfsshare /mnt/nfs/var/nfsshare/
```