# docker-compose image for Splunk + fluent-bit

This docker-compose image uses,

 - The public, official splunk enterprise image
 - The public, official splunk enterprise universalforwarder image
 - A public, unofficial fluentbit image

Bring up the containers by running,

    docker-compose build
    docker-compose up

Notes,

 - To bring down and clean up the container run `docker-compose down`

## Composition

```
,----------.    ,---.     ,---------.
|fluent-bit|    |HEC|     |Splunk UF|
|----------|--->|---|---->|---------|
`----------'    `---'     `---------'
                             |    
                             |    
       ,----------.   ,---------.
       |Splunk IDX|<--|Splunk HF|
       `----------'   `---------'
             ^                   
             |                   
       ,----------.              
       |Splunk SHC|              
       `----------'   
```

## UI   

| Function       | URL                                              |
|----------------|--------------------------------------------------|
| Splunk UI      | [http://localhost:8000/](http://localhost:8000/) |
| Splunk UF UI   | [http://localhost:8001/](http://localhost:8001/) |

The admin password for both Splunk containers is set to `admin`

## Shell

If you want to interact with the containers, run the commands below.

    ./script/shell-splunk.sh
    ./script/shell-splunkforwarder.sh
    ./script/shell-fluentbit.sh


