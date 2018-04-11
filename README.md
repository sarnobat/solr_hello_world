## Data Flow Diagram

Comment: if SOLR was designed more functionally, there would be separate jars for the indexer and for the querier. It would serve your code comprehension needs if you considered it so.

### Index-time

```
+--------------+  url + data   +-----------+  data   +-------------------------+  data   +-----------+
| command line | ------------> | http port | ------> |        solr.jar         | ------> | lucene.db |
+--------------+               +-----------+         +-------------------------+         +-----------+
                                                       ^
                                                       | analyzers (index-time)
                                                       |
                                                     +-------------------------+
                                                     |     solrconfig.xml      |
                                                     +-------------------------+
```

### Query-time
```
+---------+  url + query   +-----------+  query   +-------------------------+  query   +-----------+
| browser | -------------> | http port | -------> |        solr.jar         | -------> | lucene.db |
+---------+                +-----------+          +-------------------------+          +-----------+
                                                    ^
                                                    | analyzers (query time)
                                                    |
                                                  +-------------------------+
                                                  |     solrconfig.xml      |
                                                  +-------------------------+
```


solr_hello_world
================

# Quick start

    wget https://archive.apache.org/dist/lucene/solr/4.7.0/solr-4.7.0.zip
    sh ./solr_server_start
    sh ./solr_index_all

## Web query interface

http://localhost:8983/solr/#/collection1/query

## Command line

### Index a document

    TODO: add curl command

### Query

    TODO: add curl command
    
## Troubleshooting


Symptom - collection1 is not found in web interface (http://localhost:8983/solr/collection1)

Cause - In the console output (which I normally don't save anywhere), you see that Solr is not good at resolving symbolic links.
```
5462 [coreLoadExecutor-4-thread-1] WARN  org.apache.solr.core.SolrResourceLoader  – Can't find (or read) directory to add to classloader: ../../../contrib/extraction/lib (resolved as: /home/sarnobat/solr-4.7.0/example/example-schemaless/solr/collection1/../../../contrib/extraction/lib).
5464 [coreLoadExecutor-4-thread-1] WARN  org.apache.solr.core.SolrResourceLoader  – Can't find (or read) directory to add to classloader: ../../../dist/ (resolved as: /home/sarnobat/solr-4.7.0/example/example-schemaless/solr/collection1/../../../dist).
5465 [coreLoadExecutor-4-thread-1] WARN  org.apache.solr.core.SolrResourceLoader  – Can't find (or read) directory to add to classloader: ../../../contrib/clustering/lib/ (resolved as: /home/sarnobat/solr-4.7.0/example/example-schemaless/solr/collection1/../../../contrib/clustering/lib).
5466 [coreLoadExecutor-4-thread-1] WARN  org.apache.solr.core.SolrResourceLoader  – Can't find (or read) directory to add to classloader: ../../../dist/ (resolved as: /home/sarnobat/solr-4.7.0/example/example-schemaless/solr/collection1/../../../dist).
5467 [coreLoadExecutor-4-thread-1] WARN  org.apache.solr.core.SolrResourceLoader  – Can't find (or read) directory to add to classloader: ../../../contrib/langid/lib/ (resolved as: /home/sarnobat/solr-4.7.0/example/example-schemaless/solr/collection1/../../../contrib/langid/lib).
5480 [coreLoadExecutor-4-thread-1] WARN  org.apache.solr.core.SolrResourceLoader  – Can't find (or read) directory to add to classloader: ../../../dist/ (resolved as: /home/sarnobat/solr-4.7.0/example/example-schemaless/solr/collection1/../../../dist).
5481 [coreLoadExecutor-4-thread-1] WARN  org.apache.solr.core.SolrResourceLoader  – Can't find (or read) directory to add to classloader: ../../../contrib/velocity/lib (resolved as: /home/sarnobat/solr-4.7.0/example/example-schemaless/solr/collection1/../../../contrib/velocity/lib).
5482 [coreLoadExecutor-4-thread-1] WARN  org.apache.solr.core.SolrResourceLoader  – Can't find (or read) directory to add to classloader: ../../../dist/ (resolved as: /home/sarnobat/solr-4.7.0/example/example-schemaless/solr/collection1/../../../dist).
```


