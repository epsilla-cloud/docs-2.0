---
description: >-
  You can locally deploy the open-source Epsilla vector database by using its
  Docker image.
---

# Run with Docker

## 1. Installation

To run the pre-built Epsilla docker image on your machine, make sure Docker is installed on your system. Then download image from [Dockerhub](https://hub.docker.com/r/epsilla/vectordb).

```sh
docker pull epsilla/vectordb
```

Start the docker as the backend service

```sh
docker run --pull=always -d -p 8888:8888 epsilla/vectordb
```

Your Epsilla service is up and running. You can use REST API to interact with Epsilla, or install a Python/JavaScript client.

{% tabs %}
{% tab title="Python" %}
```bash
pip3 install --upgrade pyepsilla
```
{% endtab %}

{% tab title="JavaScript" %}
```sh
npm install epsillajs
```
{% endtab %}
{% endtabs %}

## 2. Connect to Epsilla server

{% tabs %}
{% tab title="Python" %}
```python
from pyepsilla import vectordb

## connect to vectordb
db = vectordb.Client(
  host='localhost',
  port='8888'
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const epsillajs = require('epsillajs');

// connect to vectordb
const db = new epsillajs.EpsillaDB({
  host: 'localhost',
  port: 9999
});
```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X GET "http://localhost:8888"
```

Response

```sh
Welcome to Epsilla VectorDB.
```
{% endtab %}
{% endtabs %}

Hint: if you are connecting to a secure server, use protocol parameter:

{% tabs %}
{% tab title="Python" %}
```python
db = vectordb.Client(
  protocol='https',
  host=...
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const db = new epsillajs.EpsillaDB({
    protocol: 'https',
    host: ...
});
```
{% endtab %}
{% endtabs %}

## 3. Create or load a database

{% tabs %}
{% tab title="Python" %}
```python
db.load_db(db_name="MyDB", db_path="/tmp/epsilla")
db.use_db(db_name="MyDB")
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.loadDB('/tmp/epsilla', 'MyDB');
db.useDB("MyDB");
```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X POST 'http://localhost:8888/api/load' \
    -d '{
        "path": "/tmp/epsilla",
        "name": "MyDB"
    }'
```

Response:

```json
{
    "statusCode": 200,
    "message": "Load/Create MyDB successfully."
}
```
{% endtab %}
{% endtabs %}

## 4. Create a table

{% tabs %}
{% tab title="Python" %}
```python
db.create_table(
  table_name="MyTable",
  table_fields=[
    {"name": "ID", "dataType": "INT", "primaryKey": True},
    {"name": "Doc", "dataType": "STRING"}
  ],
  indices=[
    {"name": "Index", "field": "Doc"}
  ]
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.createTable(
  'MyTable',
  [
    {"name": "ID", "dataType": "INT", "primaryKey": true},
    {"name": "Doc", "dataType": "STRING"}
  ],
  [
    {"name": "Index", "field": "Doc"}
  ]
);
```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X POST 'http://localhost:8888/api/MyDB/schema/tables' \
    -d '{
        "name": "MyTable",
        "fields": [
          {
            "name": "ID",
            "dataType": "INT",
            "primaryKey": true
          },
          {
            "name": "Doc",
            "dataType": "STRING"
          }
        ],
        "indices": [
          {
            "name": "Index",
            "field": "Doc"
          }
        ]
     }'
```

Response:

```json
{
    "statusCode":200,
    "message":"Create MyTable successfully."
}
```
{% endtab %}
{% endtabs %}

## 5. Insert new records

You can insert multiple records in a batch.

{% tabs %}
{% tab title="Python" %}
```python
db.insert(
  table_name="MyTable",
  records=[
    {"ID": 1, "Doc": "The garden was blooming with vibrant flowers, attracting butterflies and bees with their sweet nectar."},
    {"ID": 2, "Doc": "In the busy city streets, people rushed to and fro, hardly noticing the beauty of the day."},
    {"ID": 3, "Doc": "The library was a quiet haven, filled with the scent of old books and the soft rustling of pages."},
    {"ID": 4, "Doc": "High in the mountains, the air was crisp and clear, revealing breathtaking views of the valley below."},
    {"ID": 5, "Doc": "At the beach, children played joyfully in the sand, building castles and chasing the waves."},
    {"ID": 6, "Doc": "Deep in the forest, a deer cautiously stepped out, its ears alert for any signs of danger."},
    {"ID": 7, "Doc": "The old town's historical architecture spoke volumes about its rich cultural past."},
    {"ID": 8, "Doc": "Night fell, and the sky was a canvas of stars, shining brightly in the moon's soft glow."},
    {"ID": 9, "Doc": "A cozy cafe on the corner served the best hot chocolate, warming the hands and hearts of its visitors."},
    {"ID": 10, "Doc": "The artist's studio was cluttered but inspiring, filled with unfinished canvases and vibrant paints."}
  ]
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.insert('MyTable',
  [
    {"ID": 1, "Doc": "The garden was blooming with vibrant flowers, attracting butterflies and bees with their sweet nectar."},
    {"ID": 2, "Doc": "In the busy city streets, people rushed to and fro, hardly noticing the beauty of the day."},
    {"ID": 3, "Doc": "The library was a quiet haven, filled with the scent of old books and the soft rustling of pages."},
    {"ID": 4, "Doc": "High in the mountains, the air was crisp and clear, revealing breathtaking views of the valley below."},
    {"ID": 5, "Doc": "At the beach, children played joyfully in the sand, building castles and chasing the waves."},
    {"ID": 6, "Doc": "Deep in the forest, a deer cautiously stepped out, its ears alert for any signs of danger."},
    {"ID": 7, "Doc": "The old town's historical architecture spoke volumes about its rich cultural past."},
    {"ID": 8, "Doc": "Night fell, and the sky was a canvas of stars, shining brightly in the moon's soft glow."},
    {"ID": 9, "Doc": "A cozy cafe on the corner served the best hot chocolate, warming the hands and hearts of its visitors."},
    {"ID": 10, "Doc": "The artist's studio was cluttered but inspiring, filled with unfinished canvases and vibrant paints."}
  ]
);
```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X POST 'http://localhost:8888/api/MyDB/data/insert' \
  -d '{
        "table": "MyTable",
        "data": [
          {
            "ID": 1,
            "Doc": "The garden was blooming with vibrant flowers, attracting butterflies and bees with their sweet nectar."
          },
          {
            "ID": 2,
            "Doc": "In the busy city streets, people rushed to and fro, hardly noticing the beauty of the day."
          },
          {
            "ID": 3,
            "Doc": "The library was a quiet haven, filled with the scent of old books and the soft rustling of pages."
          },
          {
            "ID": 4,
            "Doc": "High in the mountains, the air was crisp and clear, revealing breathtaking views of the valley below."
          },
          {
            "ID": 5,
            "Doc": "At the beach, children played joyfully in the sand, building castles and chasing the waves."
          },
          {
            "ID": 6,
            "Doc": "Deep in the forest, a deer cautiously stepped out, its ears alert for any signs of danger."
          },
          {
            "ID": 7,
            "Doc": "The old town's historical architecture spoke volumes about its rich cultural past."
          },
          {
            "ID": 8,
            "Doc": "Night fell, and the sky was a canvas of stars, shining brightly in the moon's soft glow."
          },
          {
            "ID": 9,
            "Doc": "A cozy cafe on the corner served the best hot chocolate, warming the hands and hearts of its visitors."
          },
          {
            "ID": 10,
            "Doc": "The artist's studio was cluttered but inspiring, filled with unfinished canvases and vibrant paints."
          }
        ]
      }'          
```

Response:

```json
{
    "statusCode": 200,
    "message": "Insert data to MyTable successfully."
}
```
{% endtab %}
{% endtabs %}

## 6. Search

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.query(
  table_name="MyTable",
  query_text="Where can I find a serene environment, ideal for relaxation and introspection?",
  limit=2
)
print(response)
```

Output

```
{
  'message': 'Query search successfully.',
  'result': [
    {'Doc': 'The library was a quiet haven, filled with the scent of old books and the soft rustling of pages.', 'ID': 3},
    {'Doc': 'High in the mountains, the air was crisp and clear, revealing breathtaking views of the valley below.', 'ID': 4}
  ],
  'statusCode': 200
}
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
// search
const query = await db.query(
  'MyTable',
  {
    query: "Where can I find a serene environment, ideal for relaxation and introspection?",
    limit: 2
  }
);
console.log(JSON.stringify(query));
```

Output:

```
{
  "statusCode":200,
  "message":"Query search successfully.",
  "result":[
    {"Doc": "The library was a quiet haven, filled with the scent of old books and the soft rustling of pages.", "ID": 3},
    {"Doc": "High in the mountains, the air was crisp and clear, revealing breathtaking views of the valley below.", "ID": 4}
  ]
}
```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X POST 'http://localhost:8888/api/MyDB/data/query' \
    -d '{
        "table": "MyTable",
        "query": "Where can I find a serene environment, ideal for relaxation and introspection?",
        "limit": 2
     }'        
```

Response:

```json
{
    "statusCode": 200,
    "message": "Query search successfully.",
    "result": [
        {"Doc": "The library was a quiet haven, filled with the scent of old books and the soft rustling of pages.", "ID": 3},
        {"Doc": "High in the mountains, the air was crisp and clear, revealing breathtaking views of the valley below.", "ID": 4}
    ]
}
```
{% endtab %}
{% endtabs %}

## 7. Drop a table

{% tabs %}
{% tab title="Python" %}
```python
db.drop_table("MyTable")
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.dropTable('MyTable');
```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X DELETE 'http://localhost:8888/api/MyDB/schema/tables/MyTable'      
```

Response:

```json
{
    "statusCode": 200,
    "message": "Drop MyTable from MyDB successfully."
}
```
{% endtab %}
{% endtabs %}

## 5. Unload a database

Offload a database that is not in use to release memory (the database files are still on disk).

{% tabs %}
{% tab title="Python" %}
```python
db.unload_db("MyDB")
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.unloadDB('MyDB');
```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X POST 'http://localhost:8888/api/MyDB/unload'      
```

Response:

```json
{
    "statusCode": 200,
    "message": "Unload MyDB successfully."
}
```
{% endtab %}
{% endtabs %}

## Next steps[​](https://docs.trychroma.com/getting-started#-next-steps) <a href="#next-steps" id="next-steps"></a>

Epsilla is designed to be simple enough to get started. Refer to [Vector Database](broken-reference) for more flexibility and options on each API.

We are tirelessly working to enhance Epsilla with more features. Please consult our [Roadmap](../roadmap.md) to glimpse into the future developments.
