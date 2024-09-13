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
```bash
root@c85880676d1f:/# jmeter -n -t /test-plan/test.jmx -l /test-plan/results.csv -j /test-plan/jmeter.log
WARN StatusConsoleListener The use of package scanning to locate plugins is deprecated and will be removed in a future release
WARN StatusConsoleListener The use of package scanning to locate plugins is deprecated and will be removed in a future release
WARN StatusConsoleListener The use of package scanning to locate plugins is deprecated and will be removed in a future release
WARN StatusConsoleListener The use of package scanning to locate plugins is deprecated and will be removed in a future release
Sep 13, 2024 3:48:04 AM java.util.prefs.FileSystemPreferences$1 run
INFO: Created user preferences directory.
Creating summariser <summary>
Created the tree successfully using /test-plan/test.jmx
Starting standalone test @ 2024 Sep 13 03:48:04 UTC (1726199284997)
Waiting for possible Shutdown/StopTestNow/HeapDump/ThreadDump message on port 4445
Warning: Nashorn engine is planned to be removed from a future JDK release
summary +      1 in 00:00:00 =    2.3/s Avg:   334 Min:   334 Max:   334 Err:     0 (0.00%) Active: 1 Started: 1 Finished: 0
summary +    303 in 00:00:10 =   31.5/s Avg:    30 Min:    25 Max:   250 Err:     0 (0.00%) Active: 0 Started: 1 Finished: 1
summary =    304 in 00:00:10 =   30.2/s Avg:    31 Min:    25 Max:   334 Err:     0 (0.00%)
Tidying up ...    @ 2024 Sep 13 03:48:15 UTC (1726199295427)
... end of run
root@c85880676d1f:/# jmeter -n -t /test-plan/test.jmx -l /test-plan/results.csv -j /test-plan/jmeter.log
```


