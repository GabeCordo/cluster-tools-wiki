# HTTP Client Endpoint

The `client endpoint` is a HTTP REST port for an *operator* to interact with the core while it is operational. The endpoints runs on port `8136` by default but can be changed using the standard config file.

---

#### Processors
The endpoint returns all the processors connected to the core upon its call.

```shell
curl --location 'http://localhost:8136/processor'
```

---

#### Modules
The endpoint returns all the modules registered to the core upon its call.

```shell
curl --location 'http://localhost:8136/module'
```

#### Clusters
The endpoint shall return all clusters belonging to a module.

```shell
curl --location 'http://localhost:8136/cluster?module=common'
```

#### Mounting
The endpoint shall allow an operator to modify the mounted state of a module. *More information on mounting can be found [here](../concepts/mounting.md).*

```shell
curl --location --request PUT 'http://localhost:8136/module' \
--header 'Content-Type: application/json' \
--data '{
    "module": "common",
    "mounted": true
}'
```

```shell
curl --location --request PUT 'http://localhost:8136/cluster' \
--header 'Content-Type: application/json' \
--data '{
    "module": "common",
    "cluster": "Vec",
    "mounted": true
}'
```

---

#### Viewing Configs
The endpoint shall returns all the configs associated with a module and identifier.

```shell
curl --location 'http://localhost:8136/config?module=common&config=vec'
```

#### Creating Configs
The endpoint shall permit the operator to create a new config while the core is operational.

```shell
curl --location 'http://localhost:8136/config?module=common' \
--header 'Content-Type: application/json' \
--data '{
    "identifier": "Random",
    "on-load": "CompleteAndPush",
    "on-crash": "DoNothing",
    "start-with-n-t-channels": 3,
    "start-with-n-l-channels": 3,
    "et-channel-threshold": 2,
    "et-channel-growth-factor": 3,
    "tl-channel-threshold": 2,
    "tl-channel-growth-factor": 3
}'
```

#### Modifying Configs
The endpoint shall permit the operator to dynamically modify the config while the core is operational.

```shell
curl --location --request PUT 'http://localhost:8136/config' \
--header 'Content-Type: application/json' \
--data '{
    "identifier": "Random",
    "on-crash": 0,
    "start-with-n-t-channels": 5,
    "start-with-n-l-channels": 3,
    "et-channel-threshold": 2,
    "et-channel-growth-factor": 3,
    "tl-channel-threshold": 2,
    "tl-channel-growth-factor": 3
}'
```

#### Deleting Configs
The endpoint shall permit the operator to delete unused configs while the core is operational.

```shell
curl --location --request DELETE 'http://127.0.0.1:8136/config?module=common&config=Random'
```

---

#### Provisioning
The endpoint shall permit an operator to request the execution of a cluster's code.

```shell
curl --location 'http://localhost:8136/supervisor' \
--header 'Content-Type: application/json' \
--data '{
    "module": "common",
    "cluster": "vec",
    "config": "vec",
    "metadata": {
        "test": "hello there"
    }
}'
```

#### Supervisors
The endpoint shall permit an operator to query the state of an executed cluster.

```shell
curl --location 'http://localhost:8136/supervisor?module=common&cluster=vec'
```

---

#### Statistics
The endpoint shall return the statistics of an executed cluster.

```shell
curl --location 'http://localhost:8136/statistics?module=common&cluster=vec'
```

---

#### Viewing Cron Jobs
The endpoint shall return all the cron jobs associated with a module.

```shell
curl --location 'http://localhost:8136/job?module=common'
```

#### Creating Cron Jobs
The endpoint shall create a cron job to execute a cluster's code.

```shell
curl --location 'http://localhost:8136/job' \
--header 'Content-Type: application/json' \
--data '{
    "identifier": "test",
    "module": "common",
    "cluster": "hello",
    "config": "hello",
    "interval": {
        "minute": 10,
        "hour": 0,
        "day": 0,
        "month": 0
    },
    "metadata": {}
}'
```

#### Deleting Cron Jobs
The endpoint shall permit the operator to delete an existing cron job.

```shell
curl --location --request DELETE 'http://localhost:8136/job?id=test'
```

---

#### Toggling Debug

```shell
curl --location 'http://localhost:8136/debug' \
--header 'Content-Type: application/json' \
--data '{
    "action": "debug"
}'
```

#### Shutting Down

```shell
curl --location 'http://localhost:8136/debug' \
--header 'Content-Type: application/json' \
--data '{
    "action": "shutdown"
}'
```