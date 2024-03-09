# Processors

Processors are separate programs responsible for registering to a cluster.tools core and accepting incoming provision requests.

The core and processor communicate by exchanging messages over HTTP REST endpoints encoding objects using JSON within the request or response body.

Anyone can developer their own processor as long as it implements the interface defined by the core. This page documents the use cases and interfaces you can use as a guide to create your own processor.

If you have implemented an interface for a new language and wish to add it to this page, raise a pull request on the wiki repository.

| Language | Developer | Repository | Template |
| :- | :- | :- | :- |
| Golang | Gabriel Cordovado | https://github.com/GabeCordo/processor-framework | [goto](https://github.com/GabeCordo/processor-template)

---

## Basic Implementation

### How does the processor communicate with the core?
The processor must implement a series of functions to register itself and its callable functions with the core. Its the equipment of letting the core know you exist and what its allowed to ask you to run.

#### Connect Request
When the processor binary is started it shall create a new processor record on the core. The processor record holds two pieces of information, (1) the address the core should use when sending messages to the processor, (2) the port the processor is listening for incoming http requests.   

##### POST http://localhost:8137/processor
```json
{
    "host": "localhost",
    "port": 5023
}
```

#### Register Module Request
When the processor binary is ready to receive requests from the core it shall create a module record. The module is a grouping of functions that share a common logical purpose. Modules also contain associative metadata like version and developer contact information so a user can better understand what they are using.

In the example below, we are registering a module called _common_ that contains one function _Vec_. We set the _on-load_ specifier to _batch_ signifying that it should be user callable.

##### POST http://localhost:8137/module
```json
{
    "host": "localhost",
    "port": 5023,
    "module": {
        "config": {
            "name": "common",
            "version": 1,
            "contact": {
                "name": "James Bond",
                "email": "james.bond@gmail.com"
            },
            "exports": [
                {
                "cluster": "Vec",
                "mount": true,
                "config": {
                    "mode": "Batch",
                    "on-crash": "DoNothing",
                    "on-load": "WaitAndPush",
                    "static": {
                    "t-functions": 1,
                    "l-functions": 1
                    },
                    "dynamic": {
                    "t-function": {
                        "threshold": 2,
                        "growth-factor": 2
                    },
                    "l-function": {
                        "threshold": 2,
                        "growth-factor": 2
                    }
                    }
                }
                }
            ]
        }
    }
}
```

#### Sending Updates to the Core
TODO

---

### How does the core communicate with the processor?
The processor must implement an HTTP endpoint to receive run requests from the core.

#### Incoming Run Request

##### POST http://processor-url/supervisor
```json
{
    "module": "name",
    "cluster": "function-name",
    "config": "config-name",
    "supervisor": 0, // reference # of the run
    "metadata": {
        "key": "value"  // per-run parameters
    }
}
```

---

## Advanced Implementation
TODO

### Logging
TODO

### Caching
TODO

