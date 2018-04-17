redis-monitor
---------

base [RedisLive](https://github.com/nkrode/RedisLive)

features:
*  cluster: support thousands of redis instances
*  light: redis info base
*  metrics: memory, comands, Key HitRate, keyspace, master-slave change, expire keys
*  notification API: crash, master-slave stats changed notify

### configuration
vim src/redis_live.conf

config：

- RedisStatsServer: stats save in redis, config RedisStatsServer for stats storage backend

- others: other setttigs you can config on dashboard settings tab

samples:
```
{"master_slave_sms": "1,1",
 "RedisStatsServer": {"port": 6379, "server": "127.0.0.1"},
 "sms_alert": "192.168.110.207:9999",
 "DataStoreType": "redis",
  "RedisServers": [
  {"instance": "Master1", "group": "Test1", "port": 6379, "server": "127.0.0.1"},
  {"instance": "Slave1", "group": "Test1", "port": 6380, "server": "127.0.0.1"}
]}

```

### install deps
	pip install -r requirements.txt

### run
    # 1. start redis instance for stat stroage
    redis-server --port 6379

    # 2. start web portal
    cd src/
    python redis_live.py
    
    # 3. start stats collector daemon process
    cd src/
    python redis_monitor.py 

    # 4. dashboard: http://127.0.0.1:8888/index.html

### install centos services
    cd install/centos
    ./redis-monitor.sh

### overview
![Redis Live](https://raw.github.com/LittlePeng/redis-monitor/master/design/redis-live.png)
![Redis Live](https://raw.github.com/LittlePeng/redis-monitor/master/design/overview.png)

