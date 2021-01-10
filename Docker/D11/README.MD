## 第十一周上課

**Kubernetes安裝**

開啟三台虛擬機
- Centos7-1
- Centos7-2
- Centos7-3

`vim /etc/fstab` 註解掉swap的部分  
`vim /etc/sysctl.conf`  
貼上
```
net.ipv4.ip_forward = 1
net.bridge.bridge-nf-call-iptables = 1
```
`sysctl -p`

`yum install -y yum-utils device-mapper-persistent-data lvm2`
`vim /etc/yum.repos.d/kubernetes.repo`  
貼上
```
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
```

`yum clean all && yum repolist`
```
systemctl enable docker && systemctl start docker
yum install kubelet-1.15.2 kubectl-1.15.2 kubeadm-1.15.2 --nogpgcheck --disableexcludes=kubernetes
systemctl enable kubelet.service
```

vm1
```
kubeadm init --apiserver-advertise-address=192.168.56.117 --pod-network-cidr=10.244.0.0/16 --service-cidr=10.96.0.0/12 --kubernetes-version=v1.15.2 --cri-socket="/var/run/dockershim.sock"
```
vm1
```
mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
vm2、3
```
 kubeadm join 192.168.56.117:6443 --token a1df18.lxt11h32prkus3xx \
    --discovery-token-ca-cert-hash sha256:3f0078fe5c00917b74125620d720d78cc5396413705847ee280d4fe000ca406a
```

```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

nodeport 對外的  
port docker  
targetport 內網