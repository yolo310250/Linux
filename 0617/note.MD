## Linux 系統優化（腳本）
```
#!/bin/bash

platform=`uname -i`
if [ $platform != "x86_64" ];then
  echo "this script is only for 64bit OS"
  exit 1
fi

echo "the platform is ok"
cat << EOF
+=======================================+
| your system is CentOS 7 X86_64        |
| start optimizing........              |
+=======================================+
EOF

# add dns server
cat >> /etc/resolv.conf << EOF
nameserver 8.8.8.8
nameserver 9.9.9.9
EOF
# 在 CentOS 7 將 yum base repo 改為 hinet
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum/repos.d/CentOS-Base.repo.bak
wget -O /etc/yum.repos.d/CentOS-Base.repo http://127.0.0.1/CentOS-Base.repo
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
yum clean all
yum makecache
# 同步時間
yum -y install ntp
timedatectl set-timezone Asia/Taipei
/usr/sbin/ntpdate  tock.stdtime.gov.tw

echo "* 4 * * * /usr/sbin/ntpdate tock.stdtime.gov.tw > /dev/null 2>&1" >> /var/spool/cron/root
systemctl restart crond.service

# 限制一隻程式能打開的文件數
#echo "ulimit -SHn 102400" >> /etc/rc.local 
#cat >> /etc/security/limits.conf << EOF 
#* soft nofile 655350 
#* hard nofile 655350 
#EOF

sed -i 's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config

setenforce 0 

systemctl disable firewalld.service 
systemctl stop firewalld.service
# Linux 禁止 root 管理者以 SSH 登入
sed -i 's/#PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config
systemctl restart sshd
```
## EOF 
EOF(End OF Line) EOF常被作為檔案結束的標誌