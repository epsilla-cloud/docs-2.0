---
description: Get your cloud hosted Epsilla vector database up and running within 1 minute.
---

# Epsilla Cloud

## 1. Sign up Epsilla Cloud

Create an Epsilla Cloud account at [https://cloud.epsilla.com/](https://cloud.epsilla.com/), then sign in. You will get $25 free credit.

<figure><img src="../../.gitbook/assets/Screenshot 2023-11-21 at 9.15.04 PM.png" alt="" width="292"><figcaption></figcaption></figure>

## 2. Get your project API Key

Navigate to the 'Configurations' tab within the project, create a new API Key, and keep it at a secure place.

<figure><img src="../../.gitbook/assets/Screenshot 2023-11-21 at 9.19.00 PM.png" alt=""><figcaption></figcaption></figure>

## 3. Create a vector database, then create a table

Navigate to the 'Resource' tab, and click 'Create Vector Database'.

<figure><img src="../../.gitbook/assets/Screenshot 2023-11-21 at 9.42.30 PM.png" alt=""><figcaption></figcaption></figure>

Give the database a name, and click 'Create'. It takes a few seconds to spin up a vector database.

<figure><img src="../../.gitbook/assets/Screenshot 2023-11-21 at 9.42.46 PM.png" alt=""><figcaption></figcaption></figure>

Within the newly created database, create a new table. Give the table a name. Adjust the table schema according to your business logic, then click 'Create'.

<figure><img src="../../.gitbook/assets/Screenshot 2023-11-21 at 9.43.18 PM.png" alt=""><figcaption></figcaption></figure>

## 4. Use GUI to CRUD data to the table.

Epsilla automatically generates sample queries for the table. Start with inserting some sample data:

<figure><img src="../../.gitbook/assets/Screenshot 2023-11-21 at 9.59.56 PM.png" alt=""><figcaption></figcaption></figure>

Then query the table with top K semantic similarity search.

<figure><img src="../../.gitbook/assets/Screenshot 2023-11-21 at 10.00.21 PM (1).png" alt=""><figcaption></figcaption></figure>

Switch between Shell, Python, and JavaScript tags, and click the 'Copy' button to copy the curl command, Python code snippet, and JavaScript code snippet of the query.

<figure><img src="../../.gitbook/assets/Screenshot 2023-11-21 at 10.12.06 PM.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Copying the code snippet is the easiest way to integrate with your application as it already has the **project\_id** and **db\_id** prefilled.

Remember to replace **"YOUR-API-KEY"** part with the API Key you get earlier.
{% endhint %}

## 5. Connect to Epsilla

First, install Epsilla Python/JavaScript client.

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

Then connect to the created database.

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

## 6. Insert new records

You can insert multiple records in a batch.

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.insert(table_name="MyTable", 
  records=[
    {"ID": 1, "Doc": "Berlin", "Embedding": [0.05, 0.61, 0.76, 0.74]},
    {"ID": 2, "Doc": "London", "Embedding": [0.19, 0.81, 0.75, 0.11]},
    {"ID": 3, "Doc": "Moscow", "Embedding": [0.36, 0.55, 0.47, 0.94]},
    {"ID": 4, "Doc": "San Francisco", "Embedding": [0.18, 0.01, 0.85, 0.80]},
    {"ID": 5, "Doc": "Shanghai", "Embedding": [0.24, 0.18, 0.22, 0.44]}
  ]
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.insert('MyTable',
  [
    {"ID": 1, "Doc": "Berlin", "Embedding": [0.05, 0.61, 0.76, 0.74]},
    {"ID": 2, "Doc": "London", "Embedding": [0.19, 0.81, 0.75, 0.11]},
    {"ID": 3, "Doc": "Moscow", "Embedding": [0.36, 0.55, 0.47, 0.94]},
    {"ID": 4, "Doc": "San Francisco", "Embedding": [0.18, 0.01, 0.85, 0.80]},
    {"ID": 5, "Doc": "Shanghai", "Embedding": [0.24, 0.18, 0.22, 0.44]}
  ]
);
```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X POST 'https://api-us-east-1-1-aws.epsilla.com/api/v2/project/<PROJECT-ID>/vectordb/<DB-ID>/data/insert' \
    -H "X-API-Key: Your-API-Key-Here" \
    -H "Content-Type: application/json" \
    -d '{
        "table": "MyTable",
        "data": [
            {
              "ID": 1,
              "Doc": "Berlin",
              "Embedding": [0.05, 0.61, 0.76, 0.74]
            },
            {
              "ID": 2,
              "Doc": "London",
              "Embedding": [0.19, 0.81, 0.75, 0.11]
            },
            {
              "ID": 3,
              "Doc": "Moscow",
              "Embedding": [0.36, 0.55, 0.47, 0.94]
            },
            {
              "ID": 4,
              "Doc": "San Francisco",
              "Embedding": [0.18, 0.01, 0.85, 0.80]
            },
            {
              "ID": 5,
              "Doc": "Shanghai",
              "Embedding": [0.24, 0.18, 0.22, 0.44]
            }
         ]
     }'
```
{% endtab %}
{% endtabs %}

## 6. Search

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.query(
  table_name="MyTable",
  query_field="Embedding",
  query_vector=[0.35, 0.55, 0.47, 0.94],
  limit=2
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
// search
const query = await db.query(
  'MyTable',
  {
    queryField: "Embedding",                 // query field
    queryVector: [0.35, 0.55, 0.47, 0.94],   // query vector
    limit: 2                                 // top K
  }
);
```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X POST 'https://api-us-east-1-1-aws.epsilla.com/api/v2/project/<PROJECT-ID>/vectordb/<DB-ID>/data/query' \
    -H "X-API-Key: Your-API-Key-Here" \
    -H "Content-Type: application/json" \
    -d '{
        "table": "MyTable",
        "queryField": "Embedding",
        "queryVector": [0.35, 0.55, 0.47, 0.94],
        "limit": 2
     }'        
```
{% endtab %}
{% endtabs %}

## 7. Delete a table and delete a database

Use the GUI to delete a table and delete a database.

<figure><img src="../../.gitbook/assets/Screenshot 2023-11-21 at 10.37.57 PM.png" alt="" width="381"><figcaption></figcaption></figure>
