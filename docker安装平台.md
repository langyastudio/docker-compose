安装 CentOS 7.9.x 系统

# 基础环境

## 安装docker
在系统安装完成之后，使用 xshell 工具远程登录系统或者直接在系统的终端中进行操作
```bash
yum erase podman buildah
yum install -y yum-utils
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum install -y containerd.io docker-ce docker-ce-cli
```

依次执行上面四条命令之后，会直接进行 docker 的安装过程。在安装完成之后使用下面的命令打开 docker 的开机启动

```bash
systemctl start docker
systemctl enable docker
```


docker 参考文档 https://yeasy.gitbooks.io/docker_practice/content/



注意：如果旧版本的 Docker 为 docker or docker-engine，需要卸载：

```bash
yum remove docker \
docker-client \
docker-client-latest \
docker-common \
docker-latest \
docker-latest-logrotate \
docker-logrotate \
docker-engine
```



## 安装docker composer 

```bash
#curl -L https://github.com/docker/compose/releases/download/1.27.4/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose

# 国内用户可以使用以下方式加快下载
curl -L https://download.fastgit.org/docker/compose/releases/download/1.27.4/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose

#校验是否成功
docker-compose --version
```



## 镜像加速

针对 Docker 客户端版本大于 1.10.0 的用户，可以通过修改daemon配置文件 /etc/docker/daemon.json 来使用加速器
执行如下代码即可：[为了提高镜像下载的速度]

```bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
"registry-mirrors": ["https://4uykx8ta.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```


# 安装平台

> 磁盘挂载点 - `/mnt/volume`
>
> 如果采用smb、nfs等挂载方式，要确保共享存储的账号拥有该挂载目录的**所有者权限**

## 文件说明

- 环境服务运行脚本 `docker-compose-env.yml`



### 复制配置文件

将 `volume` 下的所有文件复制到挂载的目录 `/mnt/volume`



### 修改IP-暂时不用

`192.168.123.110` 替换为实际的 IP

```
sed -i "s/192.168.123.22/192.168.123.110/g" `grep 192.168.123.22 -rl /mnt/volume`
```



## 镜像仓库认证-暂时不用

登录阿里云 Docker Registry，密码为 xxx

```bash
docker login --username=xx registry.cn-hangzhou.aliyuncs.com
```



## 安装环境服务

执行 docker-compose up 命令即可启动依赖的所有服务

```bash
#修改权限
chmod 777 /mnt/volume/mysql
chmod 777 /mnt/volume/mysql/logs -R
chmod 777 /mnt/volume/nginx/logs -R
chmod 777 /mnt/volume/nginx/web -R
chmod 777 /mnt/volume/redis

#安装环境服务
cd /mnt/volume
docker-compose -f docker-compose-env.yml up -d
```

> mysql、redis 启动时会执行 chown 操作


### **tips**

停止所有相关容器

```bash
docker-compose -f docker-compose-app.yml stop
```

列出所有容器信息

```bash
docker-compose -f docker-compose-app.yml ps
```

