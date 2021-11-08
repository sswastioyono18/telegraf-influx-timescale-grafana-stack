# Grafana Telegraf Stack (TimescaleDB / InfluxDB)

Mostly sourced from [here for influxdb](https://github.com/bcremer/docker-telegraf-influx-grafana-stack)
and [here for timescaledb](https://github.com/Sarke/telegraf-timescaledb-docker) and upgraded the telegraf to 1.15

## Version (As of this source committed)
- Grafana 8.0.7 (will follow latest)
- Telegraf 1.18 (can be changed in [here](https://github.com/kitabisa/panduan/blob/master/docker_compose_collection/grafana-telegraf-stack/docker/Dockerfile-telegraf-timescaledb))
- Postgres 12 (you can change PG version in docker-compose)

## How to
InfluxDB
```
docker-compose -f docker-compose-influxdb.yml up -d
```

TimescaleDB
```
docker-compose -f docker-compose-timescaledb.yml up -d
```

All (in case you need both or lazy just like me). This will execute docker-compose.yml
```
docker-compose up -d
```

If you use okteto cloud, you can deploy it directly by just clicking this button
[![Develop on Okteto](https://okteto.com/develop-okteto.svg)](https://cloud.okteto.com/deploy?repository=https://github.com/sswastioyono18/compose-telegraf&branch=master)

or clone then deploy via okteto cli
```
okteto stack deploy
```

## Services and Ports

### Grafana
- URL: http://localhost:3000
- User: admin
- Password: admin

### Telegraf
- Port: 8125 (timescale) or 8126 (influx) UDP (StatsD input)

### InfluxDB
- Port: 8086 (HTTP API)
- User: admin
- Password: admin
- Database: influx

### TimescaleDB (PostgreSQL, same credentials when you want to add it into grafana)
- Port: 5433 (so it doesn't conflict with existing postgres in docker/local)
- User: root
- Password: pass
- Database: postgres

TimescaleDB will create the table based on the tag. Check telegraf-timescale.conf `table_template` parameter for more detail
