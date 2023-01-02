## install
```
#mysql 启动时会执行 chown 操作
chmod 777 ../mysql
chmod 777 ./logs
docker-compose -f docker-compose.yml up -d
```

### 数据库导入

- 将 xxx.sql 文件拷贝到 mysql 容器的 /tmp 目录下

```bash
docker cp ./db/ mysql:/tmp/
```

- 进入 mysql 容器

```bash
#进入mysql容器
docker exec -it mysql /bin/bash
cd /tmp/db
```

- 导入 db 数据

```bash
#连接到mysql服务
mysql -uroot -p --default-character-set=utf8
#输入密码 
Gl_MySQL8

#创建远程访问用户 gl，密码为 H123456a
#grant all privileges on *.* to 'gl' @'%' identified by 'H123456a';

#为了客户端的兼容性，更新一下用户的密码
#todo：未来可考虑不这样处理
#use mysql;
#ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'Gl_MySQL8';  
#FLUSH PRIVILEGES;
 
#导入sql脚本
source /tmp/db/x.x.sql;
```

## access address

```code
for native client connect port 3306
USERNAME: root
PASSWORD: Gl_MySQL8
```

