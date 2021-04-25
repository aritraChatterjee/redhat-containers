#### Configuring after startup:

First mount  the script file `conf.scr`into the container using docker volumes. Then run the following command 

```shell
$ docker exec -t <container_id> /opt/tibco/ems/8.6/bin/tibemsadmin -server tcp://localhost:7222 -script conf.scr
```

Any number of tibco ems admin commands can be added to the script file.