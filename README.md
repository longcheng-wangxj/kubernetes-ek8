# ek8v0.9_forCENTOS下载：

[下载](https://github.com/catman002/kubernetes-ek8/releases)

## ek8v0.9变化：
- 支持etcd 集群独立部署.  Support etcd cluster independent deployment
- kubernetes更新为v1.19.4.  Kubernetes updated to v1.19.4.
- docker更新为最新版本：v19.03.13-3.el7
# EK8说明：
```
Ek8[easy kubernetes]是一款快速安装和高可用性的kubernetes产品，简单易用。
通过一条命令即可完成k8s集群环境安装、配置。该产品具有以下特点：
1) 集群安装包由Kube、etcd、keepalived、haproxy、docker和docker-registry组成
2) 支持灵活的安装类型。用户可以选择全部安装或选择性安装
3) 安装程序自动检查配置。包括IP合法性，服务器连通性、帐户可用性和IP可用性
4) 支持覆盖安装和全新安装。在安装期间自动检查历史版本的有效性根据情况继续使用或更新
5) 安装程序自动设置群集服务器环境所需的环境
6) 支持远程集群安装;支持集群环境并行安装配置；
7) 支持ek8安装机和集群分离安装，ek8安装机可以是macos[version:forMAC]或支持bash的linux机器[version:forLinux]
```

- **安装前先配置 e8k.cfg 文件，设置相关服务器信息**
- **请确保ek8安装程序所在的计算机可以通过SSH无密码登录集群服务器**

```
- 当前的ek8版本是CentOS，安装机和集群服务器必须是centos7或更高版本
- 如果您需要支持k8s更高版本或支持其他服务器版本，请在GitHub上给作者留言

```

# NOTCE:

Ek8 [easy kubernetes] is a fast installation and high availability kubernetes product,
which is simple and easy to use. The product has the following features:
1) cluster installation package consists of Kube, keepalived, haproxy, docker and docker registry
2) flexible installation types are supported. Users can choose to install all or selectively by default
   according to the prepared cluster servers
3) the installation program automatically checks the configuration, including IP legality,
   IP connectivity, account availability and IP availability
4) support overlay installation. Automatically check the validity of historical version during installation and
   continue to use or update according to the situation
5) setup automatically sets the environment required for cluster server environment
6) Support ek8 installation compute and cluster separation. the compute can be macos[version:forMAC] or Bash supporting Linux machine[version:forLinux]

- to configure ek8.cfg before installation
- Please make sure that the ek8 installation compute can log on  the server through SSH without password.
- The current ek8 version is CentOS. Please confirm that the CentOS version of cluster server is V7 or higher
- This version is free. If you need a higher version, please leave a message with the author on GitHub
```
                  kubernetes version: v1.19.4
                  docker version: v19.03.13-3.el7
                  keepalived version: v2.0.19
                  haproxy version: v1.8.13
                  etcd version: v3.4.3-0
                  docker-registry: v2.0
```

# ek8 command details:

### format：ek8 command --t=type [--o=option ...]
      install command :Install cluster, command parameters include --t and --o :
               --t :Installation type, required, only one, refer to the following:
                    install: New installation. The existing cluster environment will be deleted before installation
                    initdocker: Reinstall docker only
                    initetcd: reinstall etcd only
                    initkube: Only reinstall and configure kuber
                    initkeepalived: Reinstall keepalived only
                    inithaproxy: Reinstall haproxy only
                    initregistry: Reinstall docker-registry  only
               --o :Optional, support multiple. Values are referenced below：
                    excludedocker: Only effective when '--t = initall', do not install docker
                    excludeetcd: Only effective when '--t=initall', do not install etcd
                    excluderegistry:Only effective when '--t=initall', do not install docker-registry
                    nocheckenv:Do not check the validity of cluster parameters before installation
                    only:It only takes effect when and '-t=initkube'. When initializing the Kube cluster, the required software will not be reinstalled.
      delete command  :Delete the specified configuration of kubernetes cluster. The command contains --t and --o. refer to the following:
               --t :delete type, required, only one, refer to the following::
                    cleartall: Delete cluster environment, equivalent to reset
                    cleardocker: delete docker only
                    clearetcd: delete etcd only
                    clearkube: delete kube environment  only
                    clearkeepalived: delete keepalived only
                    clearhaproxky: delete haproxy only
                    clearregistry: delete docker-registry only
               --o :Optional, support multiple. Values are referenced below：
                    excludedocker: Only effective when '--t=clearall', do not delete docker
                    excludeetcd: Only effective when '--t=clearall', do not delete etcd
                    excluderegistry: Only effective when '--t=clearall', do not delete docker-registry
                    nocheckenv: Do not check the validity of cluster parameters before deleting
      checkenv command:Only check the validity of your configuration and installation parameters, excluding --t and --o
      help command   :显示帮助。Display command instructions, excluding --t and --o
### example:
- ek8 install --t=initall . Install all software required for cluster environment (including docker, Kube, keepalived, haproxy, keepalived, registry)
- ek8 install --t=initall  --o=excludedocker . Install the software required for the cluster environment, but do not install docker. 
- ek8 install --t=initkube . Install Kebu software on cluster server only and initialize Kube environmet
- ek8 install --t=initetcd . Install Etcd software on cluster server only
- ek8 install --t=initkube  --o=only . Only Kube cluster configuration is installed, Kube software is not installed
- ek8 delete --t=clearall .  Delete all the software installed in the cluster environment, [equivalent to resetting the environment, use with caution]
- ek8 delete --t=clearall  --o=excludedocker  --o=excluderegistry . Delete all software on the cluster and reset , but do not delete docker and docker-registry
 - ek8 delete --t=clearkube .  Reset Kube cluster configuration only
- ek8 delete --t=clearhaproxy . Only delete the haproxy environment in the cluster server

### notes：
    By default, all commands in ek8 check the validity of configuration parameters. If you want to turn off, add '--o=nocheck' on the command line


# 示例：
```
- ek8 install  --t=initall。安装集群环境所需的所有软件（包括docker、Kube、keepalived、haproxy、keepalived、registry）
- ek8 install  --t=initall --o=excludedocker。安装群集环境所需的软件，但不安装docker(需确保已经安装了docker)。
- ek8 install  --t=initkube 。 仅在群集服务器上安装Kebu软件并初始化Kube环境，不安装配置其他的
- ek8 install  --t=initetcd 。 仅在群集服务器上安装etcd软件，不安装配置其他的
- ek8 install  --t=initkube --o=only。仅重新配置Kube群集配置，不安装Kube软件
- ek8 delete --t=clearall。删除群集环境中安装的所有软件，[相当于重置环境，请谨慎使用]
- ek8 delete --t=clearall --o=excludedocker--o=excluderegistry。清理集群上的所有软件和环境，但不删除docker和docker-registry
- ek8 delete --t=clearkube。仅清除Kube群集配置
- ek8 delete --t=clearhaproxy。只删除群集服务器中的haproxy环境

注意：
- 默认情况下，ek8中的所有命令都检查配置参数的有效性。如果要关闭，请在命令行中添加“--o=nocheck”

```


#
#
# ek8V0.1-centos7-kube1.15.3_forCENTOS下载：

[下载](https://github.com/catman002/kubernetes-ek8/releases/download/ek8v0.1SR/ek8V0.1-centos7-kube1.15.3_forCENTOS-20191112.tar.gz)

# EK8说明：
```
Ek8[easy kubernetes]是一款快速安装和高可用性的kubernetes产品，简单易用。
通过一条命令即可完成k8s集群环境安装、配置。该产品具有以下特点：
1) 集群安装包由Kube、keepalived、haproxy、docker和docker-registry组成
2) 支持灵活的安装类型。用户可以选择全部安装或选择性安装
3) 安装程序自动检查配置。包括IP合法性，服务器连通性、帐户可用性和IP可用性
4) 支持覆盖安装和全新安装。在安装期间自动检查历史版本的有效性根据情况继续使用或更新
5) 安装程序自动设置群集服务器环境所需的环境
6) 支持远程集群安装;支持集群环境并行安装配置；
7) 支持ek8安装机和集群分离安装，ek8安装机可以是macos[version:forMAC]或支持bash的linux机器[version:forLinux]
```

- **安装前先配置 e8k.cfg 文件，设置相关服务器信息**
- **请确保ek8安装程序所在的计算机可以通过SSH无密码登录集群服务器**

```
- 当前的ek8版本是CentOS，安装机和集群服务器必须是centos7或更高版本
- 如果您需要支持k8s更高版本或支持其他服务器版本，请在GitHub上给作者留言
```

# NOTCE:

Ek8 [easy kubernetes] is a fast installation and high availability kubernetes product,
which is simple and easy to use. The product has the following features:
1) cluster installation package consists of Kube, keepalived, haproxy, docker and docker registry
2) flexible installation types are supported. Users can choose to install all or selectively by default
   according to the prepared cluster servers
3) the installation program automatically checks the configuration, including IP legality,
   IP connectivity, account availability and IP availability
4) support overlay installation. Automatically check the validity of historical version during installation and
   continue to use or update according to the situation
5) setup automatically sets the environment required for cluster server environment
6) Support ek8 installation compute and cluster separation. the compute can be macos[version:forMAC] or Bash supporting Linux machine[version:forLinux]

- to configure ek8.cfg before installation
- Please make sure that the ek8 installation compute can log on  the server through SSH without password.
- The current ek8 version is CentOS. Please confirm that the CentOS version of cluster server is V7 or higher
- This version is free. If you need a higher version, please leave a message with the author on GitHub
```
                               kubernetes version: v1.15.3
                               docker version: v18.09.9-3.el7
                               keepalived version: v2.0.19
                               haproxy version: v1.8.13
                               docker-registry: v2.0
```

# ek8 command details:

### format：ek8 command --t=type [--o=option ...]
      install command :Install cluster, command parameters include --t and --o :
               --t :Installation type, required, only one, refer to the following:
                    install: New installation. The existing cluster environment will be deleted before installation
                    initdocker: Reinstall docker only
                    initkube: Only reinstall and configure kuber
                    initkeepalived: Reinstall keepalived only
                    inithaproxy: Reinstall haproxy only
                    initregistry: Reinstall docker-registry  only
               --o :Optional, support multiple. Values are referenced below：
                    excludedocker:Only effective when '-- t = initall', do not install docker
                    excluderegistry:Only effective when '-- t = initall', do not install docker-registry
                    nocheckenv:Do not check the validity of cluster parameters before installation
                    only:It only takes effect when and '- t = initkube'. When initializing the Kube cluster, the required software will not be reinstalled.
      delete command  :Delete the specified configuration of kubernetes cluster. The command contains --t and --o. refer to the following:
               --t :delete type, required, only one, refer to the following::
                    cleartall: Delete cluster environment, equivalent to reset
                    cleardocker: delete docker only
                    clearkube: delete kube environment  only
                    clearkeepalived: delete keepalived only
                    clearhaproxky: delete haproxy only
                    clearregistry: delete docker-registry only
               --o :Optional, support multiple. Values are referenced below：
                    excludedocker: Only effective when '--t=clearall', do not delete docker
                    excluderegistry: Only effective when '--t=clearall', do not delete docker-registry
                    nocheckenv: Do not check the validity of cluster parameters before deleting
      checkenv command:Only check the validity of your configuration and installation parameters, excluding --t and --o
      help command   :显示帮助。Display command instructions, excluding --t and --o
### example:
- ek8 install --t=initall . Install all software required for cluster environment (including docker, Kube, keepalived, haproxy, keepalived, registry)
- ek8 install --t=initall  --o=excludedocker . Install the software required for the cluster environment, but do not install docker. 
- ek8 install --t=initkube . Install Kebu software on cluster server only and initialize Kube environmet
- ek8 install --t=initkube  --o=only . Only Kube cluster configuration is installed, Kube software is not installed
- ek8 delete --t=clearall .  Delete all the software installed in the cluster environment, [equivalent to resetting the environment, use with caution]
- ek8 delete --t=clearall  --o=excludedocker  --o=excluderegistry . Delete all software on the cluster and reset , but do not delete docker and docker-registry
 - ek8 delete --t=clearkube .  Reset Kube cluster configuration only
- ek8 delete --t=clearhaproxy . Only delete the haproxy environment in the cluster server

### notes：
    By default, all commands in ek8 check the validity of configuration parameters. If you want to turn off, add '--o=nocheck' on the command line


# 示例：
```
- ek8 install  --t=initall 安装集群环境所需的所有软件（包括docker、Kube、keepalived、haproxy、keepalived、registry）
- ek8 install  --t=initall --o=excludedocker。安装群集环境所需的软件，但不安装docker(需确保已经安装了docker)。
- ek8 install  --t=initkube   仅在群集服务器上安装Kebu软件并初始化Kube环境，不安装配置其他的
- ek8 install  --t=initetcd  仅在群集服务器上安装etcd软件，不安装配置其他的
- ek8 install  --t=initkube --o=only。仅重新配置Kube群集配置，不安装Kube软件
- ek8 delete --t=clearall 删除群集环境中安装的所有软件，[相当于重置环境，请谨慎使用]
- ek8 delete --t=clearall --o=excludedocker--o=excluderegistry。清理集群上的所有软件和环境，但不删除docker和docker-registry
- ek8 delete --t=clearkube 仅清除Kube群集配置
- ek8 delete --t=clearhaproxy  只删除群集服务器中的haproxy环境

注意：
- 默认情况下，ek8中的所有命令都检查配置参数的有效性。如果要关闭，请在命令行中添加“--o=nocheck”

```
