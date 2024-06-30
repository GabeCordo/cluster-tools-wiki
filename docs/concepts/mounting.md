# Mounting

The term *mounting* is synonymous with act of making a resource available for provisioning. The term comes from the idea of mounting a server, when the server is mounted connections can begin inbound, when a server is unmounted the connections will cease. 

We choose to *mount* or *unmount* a resource based on whether we think it is a good idea to allow inbound connections. When a resource is being decommissioned or the number of faults is greater than our uptime KPI it may be beneficial to *unmount* a resource.

Since the core is a facade for provisioning resources it has the authority to decide whether to send the provision request to a processor or drop it.

## Mountable Resources

### Module
When a module is mounted, provision requests may be directed to the cluster **but** the cluster must still be mounted. When a module is un-mounted, no clusters within the module may be provisioned.  

### Cluster
When a cluster is mounted, provision requests may be directed towards a supporting processor. The module the cluster belongs to must still be mounted to access the resource.


## Observability
When a resource is mounted or un-mounted the updated status will appear in standard out.

```shell
├─ common (mounted: true) 
|  ├─vec (mounted: true)
|  |  ├─localhost:5023
|  ├─hello (mounted: true)
|  |  ├─localhost:5023
```