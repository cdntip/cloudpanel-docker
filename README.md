# 安装说明

安装基础软件

```bash
# centos 
yum install -y wget curl sudo git
# debian/ubuntu
apt update -y
apt install -y wget curl sudo git
```

安装docker
```bash
# 安装docker
curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh

# 安装 docker-compose
curl -L "https://github.com/docker/compose/releases/download/v2.23.0/docker-compose-linux-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
rm -f `which dc`
ln -s /usr/local/bin/docker-compose /usr/bin/dc
```
下载程序
```bash
git clone https://github.com/cdntip/cloudpanel-docker.git
cd cloudpanel-docker
dc up mysql -d
# 等待mysql启动之后， 再执行下面的命令
dc up -d
```
查看管理员账号
```bash
docker logs cloudpanel-api

如果显示 Can't connect to MySQL server on '177.2.0.13' ([Errno 111] Connection refused) 之类的，  执行一下 dc restart  再重新查看即可

```
添加aws镜像
```bash
# 进入容器
docker exec -it cloudpanel-api /bin/bash 

# 执行 
python manage.py aws_update_images

# 额外添加管理员
python manage.py createsuperuser --username cdntip --email cdntip@admin.com

```
在浏览器输入 ip+28080 端口即可打开
一些命令
```bash
到 cloudpanel-docker 目录

dc down  # 停止全部服务
dc up -d # 开启全部服务
dc pull # 更新镜像
dc restart # 重新创建全部服务
```
# 其它说明
目前只支持 aws、azure、linode、do （单用户）
后端暂时未上传到github, 但是代码都是未加密的, 在容器中可以看到。
docker 暂时只有x86平台(不支持arm平台)
目前版本为测试版，有问题请到群里反馈 @cdntip
