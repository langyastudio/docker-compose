## install
```
#1.0 安装mysql
#2.0 执行SQL脚本 xxl-job/db/tables_xxl_job.sql
#3.0 修改配置文件 xxl-job/conf/application.properties

#4.0 部署
chmod 777 ./logs
docker-compose -f docker-compose.yml up -d
```

## access address

```code
http://127.0.0.1:8088/xxl-job-admin/
```