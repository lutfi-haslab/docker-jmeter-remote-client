# Docker Jmeter Remote 

Author: Lutfi Ikbal Majid

### Build Jmeter base image
```bash
docker build -t jmeter-base -f Dockerfile.base .
```

### Build Docker images
```bash
docker-compose build
```

### Run Docker images
```bash
docker-compose up -d
```

### Execute Jmeter master
```bash
docker exec -it jmeter-master bash
```

### Running JMeter test plan
- Add test plan .jmx file to /test-plan directory
| Add slave client IP address to the -Rjmeter-server-1,jmeter-server-2 parameter i.e jmeter-slave-3, results name should be unique for every runs.
```bash
root@c85880676d1f:/# jmeter -n -t /test-plan/test.jmx -l /test-plan/results2.csv -j /test-plan/jmeter.log -Rjmeter-server-1,jmeter-server-2 -Dserver.rmi.ssl.disable=true
WARN StatusConsoleListener The use of package scanning to locate plugins is deprecated and will be removed in a future release
WARN StatusConsoleListener The use of package scanning to locate plugins is deprecated and will be removed in a future release
WARN StatusConsoleListener The use of package scanning to locate plugins is deprecated and will be removed in a future release
WARN StatusConsoleListener The use of package scanning to locate plugins is deprecated and will be removed in a future release
Creating summariser <summary>
Created the tree successfully using /test-plan/test.jmx
Configuring remote engine: jmeter-server-1
Configuring remote engine: jmeter-server-2
Starting distributed test with remote engines: [jmeter-server-2, jmeter-server-1] @ 2024 Sep 13 05:24:20 UTC (1726205060648)
Warning: Nashorn engine is planned to be removed from a future JDK release
Remote engines have been started:[jmeter-server-2, jmeter-server-1]
Waiting for possible Shutdown/StopTestNow/HeapDump/ThreadDump message on port 4445
summary +    403 in 00:00:10 =   39.7/s Avg:    31 Min:    24 Max:   682 Err:     0 (0.00%) Active: 1 Started: 2 Finished: 1
summary +    206 in 00:00:00 =  580.3/s Avg:    28 Min:    23 Max:    45 Err:     0 (0.00%) Active: 0 Started: 2 Finished: 2
summary =    609 in 00:00:11 =   58.0/s Avg:    30 Min:    23 Max:   682 Err:     0 (0.00%)
Tidying up remote @ 2024 Sep 13 05:24:32 UTC (1726205072942)
... end of run
root@c85880676d1f:/# exit
exit
hy4-mac-002@HY4-MAC-002 jmeter-docker % 
```

## Setting Environment
- Set RAM Size using JVM_ARGS, can be set in docker-compose.yml
```bash
JVM_ARGS=-Xms512m -Xmx1024m
```
- Add more slave clients, add this inside docker-compose.yml and make sure to change the port number. You can add as many as you want.
| Please be aware that the port number must be unique for each slave client, and JVM_ARGS must be set for each slave client and must be lower than your resource host.

```bash
jmeter-server-3:
    build:
      context: .
      dockerfile: Dockerfile.client
    container_name: jmeter-server-3
    tty: true
    networks:
      - jmeter-network
    environment:
      - JVM_ARGS=-Xms512m -Xmx1024m
    ports:
      - "50002:50000"
      - "1101:1099"
```