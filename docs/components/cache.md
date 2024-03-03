#### Cache
The ETL Framework has a built-in solution for caching intermediate data that is used in a chain of sequential ETL clusters.
This is an alternative to loading and storing data in an external database solution that introduces networking errors and latency.

##### Ensuring the Cache is Enabled
When starting up the ETL Framework on debug mode, you should see a system log notifying you that the cache thread has started.

```2023/01/25 12:37:45 (+) Cache Thread Started```

##### Cache Lifetime
Cache data is intended for short lifetime storage. This is to handle that the cache resides in system memory (which is usually limited) and
that permanent or long-term storage of data should be left to other database solutions.

**By Default Cache Records Have a Lifetime of 1 Minute**

###### Modifying the Cache Lifetime
The ETLConfig contains am "expire-in" field which specifies how many minutes should pass before a record is automatically removed from the cache.

```json
{
   "cache": {
      "expire-in": 1
   }
}
```

##### Cache Memory Usage
The cache resides in the system memory which means that the storage capabilities are highly limited versus traditional
database solutions that use disk storage. It is important we keep track of the number of cached values we store on the
ETL Cache in case developers don't realize how much data their clusters are generating, or it is being misused as a black
box for data storage.

**By Default Cache Records Have a Limit of 1000 Records**
If we have records storing 1MB of data, that is already using 1GB of system memory if maxed out.


###### Modifying the Memory Usage
The ETLConfig contains a "max-size" field in the "cache" section to change the max number of records allowed.

```json
{
   "cache": {
      "max-size": 1000
   }
}
```