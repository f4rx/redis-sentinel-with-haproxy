# Build fault-tolerance Redis cluster with Sentinel on Docker
## Topology
![topology](https://raw.githubusercontent.com/selcukusta/redis-sentinel-with-haproxy/master/redis-sentinel-mode-topology.png)
## Run
`docker-compose up -d`
## Tail sentinel logs
`clear && tail -f /var/log/sentinel.log`
## Get redis replication info per seconds
`while true; do redis-cli info replication; sleep 1; clear; done`

## Как протестировать
Запустить стенд
```bash
docker-compose up -d
sleep 15
```


После запуска на первой консоле:
```bash
docker-compose exec  proxy watch -n 1 haproxytool server -s
```

на второй:
```bash
watch -n 3 timeout 2 redis-cli info replication
```

на третьей будем выключать и включать ноду
```bash
# после этого смотреть на первоый и второй экраны - master перейдет на вторую ноду
docker-compose kill  redis01  && docker-compose rm -f redis01
# Возвращаем первую ноду в строй
docker-compose up  -d --no-recreate
```
