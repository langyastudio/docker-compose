## install
```
#https://cloud.seafile.com/published/seafile-manual-cn/docker/%E7%94%A8Docker%E9%83%A8%E7%BD%B2Seafile.md

chmod 777 ./seafile-data
#mysql 启动时会执行 chown 操作
chmod 777 ./seafile-mysql

docker-compose -f docker-compose.yml up -d
```

## access address

```code
地址：http://seafile.example.com
用户名: me@example.com
密码: d90F&zr66diwNON
```

## 配置文件
```
#https://cloud.seafile.com/published/seafile-manual-cn/config/README.md
/data/seafile/seafile-data/seafile/conf
```

## 增加一个新的管理员
确保各容器正常运行，然后执行以下命令：
```
docker exec -it seafile /opt/seafile/seafile-server-latest/reset-admin.sh
```

## 升级 Seafile 服务
```
docker pull seafileltd/seafile-mc:latest
docker compose down
docker compose up -d
```

## 垃圾回收
```
docker exec seafile /scripts/gc.sh
```