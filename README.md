# docker-compose for Splunk + fluent-bit

This docker-compose image uses,

 - [A public, official splunk enterprise image](https://hub.docker.com/r/splunk/splunk/)
 - [A public, official splunk enterprise universalforwarder image](https://hub.docker.com/r/splunk/universalforwarder/)
 - [A public, official fluentbit image](https://hub.docker.com/r/fluent/fluent-bit/)

Bring up the containers by running,

    docker-compose build
    docker-compose up

To bring down and clean up the containers run `docker-compose down`

## Composition

![fluent-bit Splunk HEC](/resource/splunk-fluentbit-components.png?raw=true "fluent-bit Splunk HEC")

```
,---------------.                   
|Logs and events|                   
`---------------'                   
      |                           
,----------.    ,---.     ,---------.
|fluent-bit|--->|HEC|---->|Splunk UF|
`----------'    `---'     `---------'
                             |    
       ,----------.   ,---------.
       |Splunk IDX|<--|Splunk HF|
       `----------'   `---------'
             ^                   
             |                   
       ,----------.   ,------.   
       |Splunk SHC|<--| User |   
       `----------'   `------'
```

The Splunk HF, IDX and SHC components are all run by the main `splunk` image.

## UI   

| Function       | URL                                              | Username  | Password |
|----------------|--------------------------------------------------|-----------|----------|
| Splunk UI      | [http://localhost:8000/](http://localhost:8000/) | admin     | admin    |

## Shell

For a shell on the containers, run the commands below.

    ./script/shell-splunk.sh
    ./script/shell-splunkforwarder.sh
    ./script/shell-fluentbit.sh

## Testing

    curl -u 'x:3e6ffd12-0f69-46bb-ad0d-71cffb661a0d' -X POST -d'{"event":"xxx"}' http://localhost:8088/services/collector/event

