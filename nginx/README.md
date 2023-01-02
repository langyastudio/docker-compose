## install
```
#修改权限
cd nginx
chmod 777 ./logs -R
chmod 777 ./web -R

#部署应用
docker-compose -f docker-compose.yml up -d
```

## access address

```code
http interface http://hostip:8700
```