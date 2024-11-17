# 安装说明

机器配置建议大于2c2g!!!

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
```
下载程序
```bash
git clone https://github.com/cdntip/cloudpanel-docker.git
cd cloudpanel-docker
docker compose up -d
```
查看管理员账号
```bash
docker logs cloudpanel-api

如果显示 Can't connect to MySQL server on '177.2.0.13' ([Errno 111] Connection refused) 之类的，  执行一下 docker compose restart  再重新查看即可

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

docker compose down  # 停止全部服务
docker compose up -d # 开启全部服务
docker compose pull # 更新镜像
docker compose restart # 重新创建全部服务
```
# 其它说明
目前只支持 aws、azure、linode、do （单用户）
后端暂时未上传到github, 但是代码都是未加密的, 在容器中可以看到。
docker 暂时只有x86平台(不支持arm平台)
目前版本为测试版，有问题请到群里反馈 @cdntip
