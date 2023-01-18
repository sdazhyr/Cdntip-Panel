# OpenFreePanel
This is a panel to manage all kinds of cloud accounts, such as az、aws、do、linode  
这个面板不适合一点linux和docker基础都没有的童鞋安装Docker  
ubuntu  18  digitalocean机器成功
### 安装docker  
curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh service docker start  
#如果docker没启动，可以运行这个  
### docker创建网络  
docker network create cdntip_network  
启动mysql容器  
mkdir /data  
docker run -d -it --network cdntip_network -v /data/mysql:/var/lib/mysql --name panel_mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=panel mysql:5.7 --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci  
(更换mysqlroot密码后，机器内部也需要修改database.conf文件的密码)  
### 启动 cloudpanel  
docker run -d -it --network cdntip_network -p 8111:80 --name panel cdntip/panel  
(8111端口可改为任意，此处为实际对外端口)
### 进入容器  
docker exec -it panel /bin/bash  
### 创建管理员  
python manage.py createsuperuser --username admin --email email@email.com
（创建用户）  
fe39SI33##3Ss3zb83  
### 添加aws镜像  
python manage.py aws_update_images   
更新程序  
docker stop panel ＃停止当前容器  
docker rm panel＃删除当前容器  
容器被关闭后，先启动数据库(panel_mysql)再启动面板(panel)

# 这些命令都是我复制粘贴的，只是排了版方便我自己粘贴到vps中，docker镜像“cdntip/panel”是作者本人的不是我自己的
备份作者的镜像：70210220/cdntip_panel
