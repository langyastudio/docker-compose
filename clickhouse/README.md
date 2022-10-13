## install
```
chmod 777 ./data
```



## access address

```code
http interface http://hostip:8123
for native client connect port 9000
```



## Upgrade this image

Step 1: update docker-compose.yml
update the value of the image property to `bitnami/clickhouse:[tag]`



Step 2: Stop and backup the currently running container
Stop the currently running container using the command

```bash
$ docker stop clickhouse
```

Next, take a snapshot of the persistent volume `/path/to/clickhouse-persistence` using:
```bash
$ rsync -a /path/to/clickhouse-persistence /path/to/clickhouse-persistence.bkp.$(date +%Y%m%d-%H.%M.%S)
```


Step 3: Remove the currently running container

```bash
$ docker rm -v clickhouse
```


Step 4: Run the new image
Re-create your container from the new image

```bash
$ docker-compose up clickhouse
```
