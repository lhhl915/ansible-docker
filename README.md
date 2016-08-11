## **==亚信paas平台openshift环境，ansible初始化剧本（playbook)==**

###### mail:liuhl3@asiainfo.com
###### version:1.0.0
###### name：hailongliu

---

## 前提：
- ansible已安装并且版本1.9.0以上（推荐：yum安装）
- master & node 系统必须是Centos 7
- 保证联网而且master与node节点间能够正常通信(ping)
- 防火墙设置正确
- 

```
ansible --version    #主节点ansible版本
cat /etc/redhat-release  #所有节点系统版本
```


---

## 1.下载代码：
git clone https://github.com/lhhl915/ansible-docker.git
cd ansible-docker

---
## 2.编辑ansible inventory文件

```
vim ansible_playbook/inventory

[install]
192.168.11.18  ansible_ssh_pass=ssh_passwd
192.168.11.19  ansible_ssh_pass=ssh_passwd
```


---

## 3.执行一键初始化剧本(playbook)
ansible-playbook -i ./ansible_playbook/inventory ./ansible_playbook/playbook.yml


### ==**特别注意:**==
- 忽略执行过程中的错误提示
- docker能否启动成功与其他因素有关（例子：网易云平台的话需要绑定ip）

## 4.以下为细化的过程

*****************升级openssl:*****************


```
cd ./ansible-docker/roles/openssl_repair
```

将openssl版本升级到"openssl-1.0.2h"

*************初始化openshift环境:*************


```
cd ./ansible-docker/roles/openshift_install
```
yum update

openshift依赖包安装

*****************安装docker:*****************


```
cd ./ansible-docker/roles/docker_install
```

安装docker-1.9.1-25


**************open-falcon节点安装:**************


```
cd ./ansible-docker/roles/open-falcon_node_install
```
上传agent客户端

