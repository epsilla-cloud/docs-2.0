# Performance Tuning

Starting in 0.3.9, Epsilla Vector Database offers advanced performance tuning options to cater to diverse operational needs, ensuring optimal efficiency and speed for vector data processing. By adjusting the configuration through a simple POST request to the API endpoint, users can fine-tune the database's performance to their specific requirements:

```sh
curl -X POST 'http://localhost:8888/api/config' \
    -d '{
        "IntraQueryThreads": 4,
        "ConcurrentWorkersPerIndex": 16,
        "RebuildThreads": 1,
        "SearchQueueSize": 500
    }'
```

Note: all the config entries are optional. If not provided, the entry value will stay as default (shown in the table below).

Here's a table that succinctly presents the performance tuning parameters supported by Epsilla Vector Database:

<table><thead><tr><th width="260">Parameter</th><th width="134">Default Value</th><th>Description</th></tr></thead><tbody><tr><td>IntraQueryThreads</td><td>4</td><td>Controls the number of threads used within a single query, enabling efficient parallel processing for a single vector search query. Set a larger value to get a lower query latency. Note: increasing the value will reduce the throughput the whole system can handle.</td></tr><tr><td>ConcurrentWorkersPerIndex</td><td>16</td><td>Sets the number of concurrent workers. Enables concurrent query processing. Set to a larger value to get better throughput. Note: <code>IntraQueryThreads * ConcurrentWorkersPerIndex</code> should not exceed <code>Total available threads - RebuildThreads</code>, otherwise the increased context switch will reduce the overall system performance.</td></tr><tr><td>RebuildThreads</td><td>1</td><td>Determines the number of threads allocated for rebuilding vector indexes. Set to a larger value to get a faster indexing rebuild.</td></tr><tr><td>SearchQueueSize</td><td>500</td><td>Adjusts the size of the search queue. The larger the value, the higher the recall of vector search (especially in metadata filtering), with a tradeoff of higher query latency.</td></tr></tbody></table>

