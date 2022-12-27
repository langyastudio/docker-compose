## install
```
#1.安装 MySQL 并导入 SQL 脚本
./sql/apolloconfigdb.sql 
./sql/apolloportaldb.sql

#2.修改docker-compose.yml的数据库连接信息

#3.部署应用
docker-compose -f docker-compose.yml up -d
```

## access address

```code
http interface http://hostip:8070
用户名 apollo，密码 admin

http://hostip:8080 http://hostip:8090
```

## build
- from: https://github.com/apolloconfig/apollo-quick-start
- modify demo.sh file:
```bash
if [[ -n "$APOLLO_CONFIG_DB_URL" ]]; then
  echo APOLLO_CONFIG_DB_URL = "$APOLLO_CONFIG_DB_URL"
fi

if [[ -n "$APOLLO_CONFIG_DB_USERNAME" ]]; then
  echo APOLLO_CONFIG_DB_USERNAME = "$APOLLO_CONFIG_DB_USERNAME"
fi

if [[ -n "$APOLLO_CONFIG_DB_PASSWORD" ]]; then
  echo APOLLO_CONFIG_DB_PASSWORD = "${APOLLO_CONFIG_DB_PASSWORD//?/*}"
fi

if [[ -n "$APOLLO_PORTAL_DB_URL" ]]; then
  echo APOLLO_PORTAL_DB_URL = "$APOLLO_PORTAL_DB_URL"
fi

if [[ -n "$APOLLO_PORTAL_DB_USERNAME" ]]; then
  echo APOLLO_PORTAL_DB_USERNAME = "$APOLLO_PORTAL_DB_USERNAME"
fi

if [[ -n "$APOLLO_PORTAL_DB_PASSWORD" ]]; then
  echo APOLLO_PORTAL_DB_PASSWORD = "${APOLLO_PORTAL_DB_PASSWORD//?/*}"
fi

# apollo config db info
apollo_config_db_url="jdbc:mysql://$APOLLO_CONFIG_DB_URL"
apollo_config_db_username=${APOLLO_CONFIG_DB_USERNAME:-root}
apollo_config_db_password=${APOLLO_CONFIG_DB_PASSWORD:-}

# apollo portal db info
apollo_portal_db_url="jdbc:mysql://$APOLLO_PORTAL_DB_URL"
apollo_portal_db_username=${APOLLO_PORTAL_DB_USERNAME:-root}
apollo_portal_db_password=${APOLLO_PORTAL_DB_PASSWORD:-}
```

- build image
```bash
chmod +x demo.sh
docker build . -t apollo-quick-start:2.0.1
``` 