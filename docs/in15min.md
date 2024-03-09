# Get Upto Speed in 15 Minutes

The cluster.tools core is a _cloud_ orchestration tool for Lambda and ETL functions. The power of the core is through handling multiple functionalities that are required for cloud pipelines but distract developers from building the transformations functions that are most important for business or product requirements.


[show core and processors]


It is important to note that the core itself does not provision (execute) any code itself, but rather is responsible for distributing calls to executables called _processors_ that are responsible for providing a common interface for the core to call code. The interface between the core and processor is an HTTP REST API that accepts data in a JSON format for sending/receiving content. The details of the interface are described in more detail within the _processor_ page.

[what is a cluster, how it works]

[how modules isolate clusters]

[versioning to support multiple versions]

[mounting / unmounting]

[provisioning]


Some of the functionality includes:
1. Dynamic Registering of Processors
2. Encapsulation/Isolation of Code into Register-able Modules 
3. Module Versioning
4. Dynamic Availability through Mounting and Unmounting
4. Remote Procedure Calls
5. Load Balancing Across Processors with a common registered module
3. Configuration Management
4. Short Term Caching
5. Statistic Monitoring