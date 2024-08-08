# docker-installer
> Docker 官方安装包，用于解决大清无法访问 Docker 官网下载安装的问题

6月以来，大量Docker镜像网站停服，Docker无法下载安装<br>
本仓库致力于解决国内网络原因无法使用Docker的问题。<br>

### 特点：
- 使用Github Action将官网的安装脚本/安装包定时下载到本项目Release，供国内使用<br>
- 官方安装包，安全可靠<br>
- 每天自动定时同步，保证最新<br>

# 1. Docker安装
## 1.1 Linux
一键安装命令（每天自动从官网定时同步）
```
sudo curl -fsSL https://github.com/yhyzgn/docker-installer/releases/download/latest/linux.sh | bash -s docker --mirror Aliyun
```

> 备用（如果Github访问不了，可以使用Ghproxy的链接）<br>
```
sudo curl -fsSL https://mirror.ghproxy.com/https://github.com/yhyzgn/docker-installer/releases/download/latest/linux.sh | bash -s docker --mirror Aliyun
```

> 再备用（如果还是不行，就使用Gitee的链接吧）<br>
```
sudo curl -fsSL https://gitee.com/yhyzgn/docker-installer/releases/download/latest/linux.sh | bash -s docker --mirror Aliyun
```
启动docker
```
sudo service docker start
```

## 1.2 Windows
任务栏搜索功能，启用"适用于Linux的Windows子系统" + "虚拟机平台" <br>
![](images/windows功能.png)

管理员权限打开命令提示符，安装wsl2<br>
```
wsl --set-default-version 2
wsl --update --web-download
```
等待wsl安装成功
![](images/wsl2成功.png)
下载Windows版本安装包，进入此项目的Release<br>
https://github.com/yhyzgn/docker-installer/releases

下载Windows版本安装包
![](images/windows安装包.png)
双击安装即可

>可选:
如果想自己指定安装目录，可以使用命令行的方式
参数 --installation-dir=D:\Docker可以指定安装位置


```
start /w "" "Docker Desktop Installer.exe" install --installation-dir=D:\Docker
```

## 1.3 Mac
进入此项目的Release，下载Mac系统的安装包<br>
https://github.com/yhyzgn/docker-installer/releases
![](images/mac安装包.png)
注意区分CPU架构类型 Intel芯片选择x86_64, 苹果芯片选择arm64<br>
下载好双击安装即可

# 2. Pull镜像

### 方案一  转存到阿里云
使用Github Action将国外的Docker镜像转存到阿里云私有仓库，供国内服务器使用，免费易用

- 支持DockerHub, gcr.io, k8s.io, ghcr.io等任意仓库
- 支持最大40GB的大型镜像
- 使用阿里云的官方线路，速度快

项目地址: 
https://github.com/yhyzgn/docker-image-pusher

### 方案二 镜像站
现在只有很少的国内镜像站存活<br>
不保证镜像齐全,且用且珍惜<br>
以下三个镜像站背靠较大的开源项目，优先推荐<br>

|项目名称|项目地址| 加速地址|
| ----------- | ----------- |----------- |
|1Panel|[https://github.com/1Panel-dev/1Panel/](https://github.com/1Panel-dev/1Panel/)|https://docker.1panel.live|
|Daocloud|[https://github.com/DaoCloud/public-image-mirror](https://github.com/DaoCloud/public-image-mirror)|https://docker.m.daocloud.io|
|耗子面板|[https://github.com/TheTNB/panel](https://github.com/TheTNB/panel 	)|https://hub.rat.dev|


#### Linux配置镜像站
```
sudo vi /etc/docker/daemon.json
```
输入下列内容，最后按ESC，输入 :wq! 保存退出。
```
{
    "registry-mirrors": [
        "https://docker.m.daocloud.io",
        "https://docker.1panel.live",
        "https://hub.rat.dev"
    ]
}
```
重启docker
```
sudo service docker restart
```

#### Windows/Mac配置镜像站
Setting->Docker Engine->添加上换源的那一段，如下图
![](images/win加速.png)

### 方案三 离线镜像
使用Github Action下载docker离线镜像
https://github.com/wukongdaily/DockerTarBuilder

### 方案四 使用一键脚本
bash -c "$(curl -sSLf https://xy.ggbond.org/xy/docker_pull.sh)" -s 完整镜像名

### 方案五 使用Cloudflare worker 自建镜像加速
https://github.com/cmliu/CF-Workers-docker.io

# 3. 去哪里找镜像

https://docker.fxxk.dedyn.io/
