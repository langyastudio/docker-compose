## 方案1、standalone install 
```
#部署应用
docker-compose -f docker-compose.yml up -d
```

## 方案2、standalone&mysql install
```
#1.1 安装mysql，略

#1.2 导入数据
#https://raw.githubusercontent.com/alibaba/nacos/develop/distribution/conf/mysql-schema.sql
将 nacos/env/mysql-schema.sql 脚本导入 mysql 数据库

#2.1 修改配置，修改 nacos/env/nacos-standlone-mysql.env 文件的数据库配置信息
#MYSQL_SERVICE_HOST 可以改为 IP

#2.2 部署应用
chmod 777 ./logs
docker-compose -f docker-compose-mysql.yml up -d
```

## access address

```code
地址: hostip:8848/nacos
用户名: nacos
密码: nacos
```



