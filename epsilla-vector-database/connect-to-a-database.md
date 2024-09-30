---
description: >-
  In Epsilla, the data are organized as databases. A database is consisted of
  multiple tables.
---

# Connect to a database

{% hint style="info" %}
There is a slightly difference between Docker and Epsilla Cloud when connecting to a database.
{% endhint %}

## Connect to a database using Epsilla Docker

### Step 0. Download docker image and start

Epsilla vector database docker images can be found at [docker hub](https://hub.docker.com/r/epsilla/vectordb).

Use the command below to pull the latest version of Epsilla vector DB:

```sh
docker pull epsilla/vectordb
```

You can also specify the version to pull:

```bash
docker pull epsilla/vectordb:0.3.1
```

Start the docker as the backend service

```sh
docker run --pull=always -d -p 8888:8888 epsilla/vectordb
```

Use the EMBEDDING\_MODELS environment variable to enable more built-in embedding models (learn more about [embeddings](embeddings.md)):

```bash
docker run --pull=always -d -p 8888:8888 -e EMBEDDING_MODELS="BAAI/bge-small-zh-v1.5,BAAI/bge-base-en" epsilla/vectordb
```

### Step 1. Initialize Client

{% tabs %}
{% tab title="Python" %}
```python
### client connect to localhost
from pyepsilla import vectordb
db = vectordb.Client()


### client connect to remote server
from pyepsilla import vectordb
db = vectordb.Client(
    protocol='http',      # http or https. Default is http
    host='3.100.100.100', # The host machine for the vector db. Default localhost
    port='8888'           # The port for the vector db, default 8888
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
// client connect to localhost
const epsillajs = require('epsillajs');
const db = new epsillajs.EpsillaDB();

// client connect to remote server
const epsillajs = require('epsillajs');
const db = new epsillajs.EpsillaDB({
    protocol: 'http',      // http or https. Default is http
    host: '3.100.100.100', // The host machine for the vector db. Default localhost
    port: '8888'           // The port for the vector db, default 8888
});
```
{% endtab %}
{% endtabs %}

In order to use OpenAI for embedding, pass in X-OpenAI-API-Key header:

{% tabs %}
{% tab title="Python" %}
```python
db = vectordb.Client(
    ...
    headers={
        "X-OpenAI-API-Key": <Your OpenAI API key here>
    }
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const db = new epsillajs.EpsillaDB({
    ...
    headers: {
        "X-OpenAI-API-Key": <Your OpenAI API key here>
    }
});
```
{% endtab %}
{% endtabs %}

### Step 2. Load database

Use the command to load a database into memory. Epsilla can hold multiple databases in memory at the same time.

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.load_db(
    db_name="myDB",         # The name of the DB. Can give any valid
                            # name when loading a DB from disk.
    db_path="/tmp/epsilla", # The path on the disk where the DB is persisted. 
                            # If the path doesn't exist, will create
                            # a new DB at this path.
    vector_scale=1000000,   # (Optional) the limit of the number of records in
                            # the table. Can provide any positive number at
                            # load_db time. If not specified, the default value
                            # is 150000.
    wal_enabled=True        # (Optional) Enable write ahead log or not. Default 
                            # is True. For high throughput low consistency case,
                            # can disable it to save disk IO.
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const load = await db.loadDB(
    "/tmp/epsilla", // The path on the disk where the DB is persisted. 
                    // If the path doesn't exist, will create
                    // a new DB at this path.
    "MyDB",         // The name of the DB. Can give any valid
                    // name when loading a DB from disk.
    1000000,        // (Optional) the limit of the number of records in
                    // the table. Can provide any positive number at
                    // loadDB time. If not specified, the default value
                    // is 150000.
    true            // (Optional) Enable write ahead log or not. Default 
                    // is True. For high throughput low consistency case,
                    // can disable it to save disk IO.
);
```
{% endtab %}
{% endtabs %}

### Step 3. Use database

You can use the command to switch between multiple databases that are already loaded in memory. Then the following interactions will be towards this database.

{% tabs %}
{% tab title="Python" %}
```python
db.use_db(db_name="myDB")
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
db.useDB("MyDB");
```
{% endtab %}
{% endtabs %}

## Connect to a vector database on Epsilla Cloud

First, create a vector database on Cloud GUI.

<figure><img src="../.gitbook/assets/Screenshot 2023-11-21 at 9.42.30 PM.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
We will support creating vector databases via Python/JavaScript client in the near future.
{% endhint %}

Then connect to the created database. Replace the Project ID, Database ID and API Key.

{% tabs %}
{% tab title="Python" %}
```python
from pyepsilla import cloud
client = cloud.Client(
  project_id="PROJECT-ID",     # Copied from the GUI code snippet
  api_key="YOUR-API-KEY"       # Replace with your API Key
)
db = client.vectordb(db_id="DB-ID") # Copied from the GUI code snippet
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const epsillajs = require('epsillajs');
const client = new epsillajs.EpsillaCloud({
  projectID: 'PROJECT-ID',  // Copied from the GUI code snippet
  apiKey: 'YOUR-API-KEY'    // Replace with your API Key
});
const db = new epsillajs.VectorDB(
  'DB-ID',                  // Copied from the GUI code snippet
   client
 ); 
await db.connect();
```
{% endtab %}
{% endtabs %}

The Project ID and Database ID can be copied from the database card under project resources:

<figure><img src="../.gitbook/assets/Screenshot 2023-11-22 at 10.28.27 AM.png" alt=""><figcaption></figcaption></figure>

The API Key can be created under project configurations:

<figure><img src="../.gitbook/assets/Screenshot 2023-11-21 at 9.19.00 PM.png" alt=""><figcaption></figcaption></figure>
