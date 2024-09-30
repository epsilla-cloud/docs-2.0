# Embeddings

Embeddings/vectors are numerical representations of complex data like text or images in a format that machines can process. Embedding models convert text, images, audios, and videos into vectors of real numbers. This process captures semantic meaning, allowing algorithms to understand content similarity and context. This technique is pivotal in various applications, from Retrieval Augmented Generation (RAG) to recommendation systems to language translation, as it enables computers to 'understand' and work with human language.

<figure><img src="../.gitbook/assets/Screenshot 2023-12-18 at 1.56.44 PM.png" alt=""><figcaption></figcaption></figure>

In embedding models, the mathematical premise is that the closer two vectors are in high-dimensional space, the more semantically similar they are. This characteristic is leveraged in vector databases for semantic similarity search, using algorithms like nearest neighbor search. These algorithms compute the distances between vectors, interpreting smaller distances as higher similarity. This approach enables applications to find closely related items (like texts, images, audios, videos) based on their embedded vector representations, making it possible to conduct searches and analyses based on the meaning and context of the data, rather than just literal matches.

<figure><img src="../.gitbook/assets/Screenshot 2023-12-18 at 3.19.33 PM.png" alt=""><figcaption></figcaption></figure>

## Use Embeddings

Starting in v0.3, Epsilla supports automatically embed your documents and questions within the vector database, which significantly simplify the end to end semantic similarity search workflow.

When creating tables, you can define indices to let Epsilla automatically create embeddings for the STRING fields:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.create_table(
    table_name="MyTable",
    table_fields=[
        {"name": "ID", "dataType": "INT", "primaryKey": True},
        {"name": "Doc", "dataType": "STRING"}
    ],
    indices=[
        {"name": "Index", "field": "Doc", "model": "BAAI/bge-small-en-v1.5"}
    ]
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.createTable('MyTable',
  [
    {"name": "ID", "dataType": "INT", "primaryKey": true},
    {"name": "Doc", "dataType": "STRING"}
  ],
  [
    {"name": "Index", "field": "Doc", "model": "BAAI/bge-small-en-v1.5"}
  ]
);
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
You can omit the model when defining indices, and Epsilla uses BAAI/bge-small-en-v1.5 by default.
{% endhint %}

Then you can insert records in their raw format and let Epsilla handle the embedding:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.insert(
  table_name="MyTable",
  records=[
    {"ID": 1, "Doc": "The garden was blooming with vibrant flowers, attracting butterflies and bees with their sweet nectar.", "Embedding": [0.05, 0.61, 0.76, 0.74]},
    {"ID": 2, "Doc": "In the busy city streets, people rushed to and fro, hardly noticing the beauty of the day.", "Embedding": [0.19, 0.81, 0.75, 0.11]},
    {"ID": 3, "Doc": "The library was a quiet haven, filled with the scent of old books and the soft rustling of pages.", "Embedding": [0.36, 0.55, 0.47, 0.94]},
    {"ID": 4, "Doc": "High in the mountains, the air was crisp and clear, revealing breathtaking views of the valley below.", "Embedding": [0.18, 0.01, 0.85, 0.80]},
    {"ID": 5, "Doc": "At the beach, children played joyfully in the sand, building castles and chasing the waves.", "Embedding": [0.24, 0.18, 0.22, 0.44]}
  ]
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.insert('MyTable',
  [
    {"ID": 1, "Doc": "The garden was blooming with vibrant flowers, attracting butterflies and bees with their sweet nectar.", "Embedding": [0.05, 0.61, 0.76, 0.74]},
    {"ID": 2, "Doc": "In the busy city streets, people rushed to and fro, hardly noticing the beauty of the day.", "Embedding": [0.19, 0.81, 0.75, 0.11]},
    {"ID": 3, "Doc": "The library was a quiet haven, filled with the scent of old books and the soft rustling of pages.", "Embedding": [0.36, 0.55, 0.47, 0.94]},
    {"ID": 4, "Doc": "High in the mountains, the air was crisp and clear, revealing breathtaking views of the valley below.", "Embedding": [0.18, 0.01, 0.85, 0.80]},
    {"ID": 5, "Doc": "At the beach, children played joyfully in the sand, building castles and chasing the waves.", "Embedding": [0.24, 0.18, 0.22, 0.44]}
  ]
);
```
{% endtab %}
{% endtabs %}

After inserting records, you can query the table with natural language questions:

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
{% endtabs %}

## Built-in Embeddings

Here is the list of built-in embedding models Epsilla supports:

* BAAI/bge-small-en
* BAAI/bge-small-en-v1.5
* BAAI/bge-small-zh-v1.5
* BAAI/bge-base-en
* BAAI/bge-base-en-v1.5
* sentence-transformers/all-MiniLM-L6-v2

**BAAI/bge-small-en-v1.5** and **sentence-transformers/all-MiniLM-L6-v2** are enabled by default. You can turn on other models via docker run command environment variable EMBEDDING\_MODELS (using comma separated string):

```bash
docker run --pull=always -d -p 8888:8888 -e EMBEDDING_MODELS="BAAI/bge-small-zh-v1.5,BAAI/bge-base-en" epsilla/vectordb
```

When using these built-in embedding models, the embedding are conducted within your local laptop without outbound network. They use CPU first to do the embedding. So make sure you have enough CPU power and memory to handle the models before enabling them.

## OpenAI Embedding

Epsilla supports these OpenAI embedding models:

<table><thead><tr><th width="313">Name</th><th width="134">Dimensions</th><th>Support Dimension Reduction</th></tr></thead><tbody><tr><td><strong>openai/text-embedding-3-large</strong></td><td>3072</td><td>Yes</td></tr><tr><td><strong>openai/text-embedding-3-small</strong></td><td>1536</td><td>Yes</td></tr><tr><td><strong>openai/text-embedding-ada-002</strong></td><td>1536</td><td>No</td></tr></tbody></table>

When using OpenAI embedding on Docker, make sure provide the **X-OpenAI-API-Key** header when connecting to the vector database:

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

{% hint style="info" %}
If you are using Epsilla Cloud, make sure to add [OpenAI integration](integrations/openai.md) instead of passing the header.
{% endhint %}

And use the embedding model when defining the index:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.create_table(
    ...
    indices=[
        {"name": "Index", "field": "Doc", "model": "openai/text-embedding-3-large"}
    ]
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.createTable(
  ...
  [
    {"name": "Index", "field": "Doc", "model": "openai/text-embedding-ada-002"}
  ]
);
```
{% endtab %}
{% endtabs %}

## Jina AI Embedding

Epsilla supports these JinaAI embedding models (learn more about Jina AI embedding at [https://jina.ai/embeddings/](https://jina.ai/embeddings/)):

| Name                                    | Dimensions |
| --------------------------------------- | ---------- |
| **jinaai/jina-embeddings-v2-base-en**   | 768        |
| **jinaai/jina-embeddings-v2-base-de**   | 768        |
| **jinaai/jina-embeddings-v2-base-zh**   | 768        |
| **jinaai/jina-embeddings-v2-base-code** | 768        |
| **jinaai/jina-embeddings-v2-small-en**  | 512        |

When using Jina AI embedding on Docker, make sure provide the **X-JinaAI-API-Key** header when connecting to the vector database:

{% tabs %}
{% tab title="Python" %}
```python
db = vectordb.Client(
    ...
    headers={
        "X-JinaAI-API-Key": <Your Jina AI API key here>
    }
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const db = new epsillajs.EpsillaDB({
    ...
    headers: {
        "X-JinaAI-API-Key": <Your Jina AI API key here>
    }
});
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you are using Epsilla Cloud, make sure to add [JinaAI integration](integrations/jina-ai.md) instead of passing the header.
{% endhint %}

And use the embedding model when defining the index:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.create_table(
    ...
    indices=[
        {"name": "Index", "field": "Doc", "model": "jinaai/jina-embeddings-v2-base-en"}
    ]
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.createTable(
  ...
  [
    {"name": "Index", "field": "Doc", "model": "jinaai/jina-embeddings-v2-base-en"}
  ]
);
```
{% endtab %}
{% endtabs %}

## Voyage AI Embedding

Epsilla supports these VoyageAI embedding models (learn more about Voyage AI embedding at [https://www.voyageai.com/](https://www.voyageai.com/)):

| Name                                 | Dimensions |
| ------------------------------------ | ---------- |
| **voyageai/voyage-large-2**          | 1536       |
| **voyageai/voyage-code-2**           | 1536       |
| **voyageai/voyage-2**                | 1024       |
| **voyageai/voyage-02**               | 1024       |
| **voyageai/voyage-law-2**            | 1024       |
| **voyageai/voyage-finance-2**        | 1024       |
| **voyageai/voyage-multilingual-2**   | 1024       |
| **voyageai/voyage-lite-02-instruct** | 1024       |
| **voyageai/voyage-3**                | 1024       |
| **voyageai/voyage-3-lite**           | 512        |

When using Voyage AI embedding on Docker, make sure provide the **X-VoyageAI-API-Key** header when connecting to the vector database:

{% tabs %}
{% tab title="Python" %}
```python
db = vectordb.Client(
    ...
    headers={
        "X-VoyageAI-API-Key": <Your Voyage AI API key here>
    }
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const db = new epsillajs.EpsillaDB({
    ...
    headers: {
        "X-VoyageAI-API-Key": <Your Voyage AI API key here>
    }
});
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you are using Epsilla Cloud, make sure to add [VoyageAI integration](integrations/voyage-ai.md) instead of passing the header.
{% endhint %}

And use the embedding model when defining the index:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.create_table(
    ...
    indices=[
        {"name": "Index", "field": "Doc", "model": "voyageai/voyage-02"}
    ]
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.createTable(
  ...
  [
    {"name": "Index", "field": "Doc", "model": "voyageai/voyage-02"}
  ]
);
```
{% endtab %}
{% endtabs %}

## Mixedbread AI Embedding

Epsilla supports these Mixedbread AI embedding models (learn more about Mixedbread AI embedding at [https://www.mixedbread.ai/docs/models/embeddings#models](https://www.mixedbread.ai/docs/models/embeddings#models)):

| Name                                   | Dimensions |
| -------------------------------------- | ---------- |
| **mixedbreadai/UAE-Large-V1**          | 1024       |
| **mixedbreadai/bge-large-en-v1.5**     | 1024       |
| **mixedbreadai/gte-large**             | 1024       |
| **mixedbreadai/e5-large-v2**           | 1024       |
| **mixedbreadai/multilingual-e5-large** | 1024       |
| **mixedbreadai/multilingual-e5-base**  | 768        |
| **mixedbreadai/gte-large-zh**          | 1024       |

When using Mixedbread AI embedding on Docker, make sure provide the **X-MixedbreadAI-API-Key** header when connecting to the vector database:

{% tabs %}
{% tab title="Python" %}
```python
db = vectordb.Client(
    ...
    headers={
        "X-MixedbreadAI-API-Key": <Your Mixedbread AI API key here>
    }
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const db = new epsillajs.EpsillaDB({
    ...
    headers: {
        "X-MixedbreadAI-API-Key": <Your Mixedbread AI API key here>
    }
});
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you are using Epsilla Cloud, make sure to add [Mixedbread AI integration](integrations/mixedbread-ai.md) instead of passing the header.
{% endhint %}

And use the embedding model when defining the index:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.create_table(
    ...
    indices=[
        {"name": "Index", "field": "Doc", "model": "mixedbreadai/UAE-Large-V1"}
    ]
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.createTable(
  ...
  [
    {"name": "Index", "field": "Doc", "model": "mixedbreadai/UAE-Large-V1"}
  ]
);
```
{% endtab %}
{% endtabs %}

## Nomic AI Embedding

Epsilla supports these Nomic AI embedding models (learn more about Nomic AI embedding at [https://docs.nomic.ai/reference/endpoints/nomic-embed-text](https://docs.nomic.ai/reference/endpoints/nomic-embed-text)):

| Name                              | Dimensions |
| --------------------------------- | ---------- |
| **nomicai/nomic-embed-text-v1.5** | 768        |
| **nomicai/nomic-embed-text-v1**   | 768        |

When using Nomic AI embedding on Docker, make sure provide the **X-NOMIC-API-Key** header when connecting to the vector database:

{% tabs %}
{% tab title="Python" %}
```python
db = vectordb.Client(
    ...
    headers={
        "X-NOMIC-API-Key": <Your Nomic AI API key here>
    }
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const db = new epsillajs.EpsillaDB({
    ...
    headers: {
        "X-NOMIC-API-Key": <Your Nomic AI API key here>
    }
});
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you are using Epsilla Cloud, make sure to add [Nomic AI integration](integrations/nomic-ai.md) instead of passing the header.
{% endhint %}

And use the embedding model when defining the index:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.create_table(
    ...
    indices=[
        {"name": "Index", "field": "Doc", "model": "nomicai/nomic-embed-text-v1"}
    ]
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.createTable(
  ...
  [
    {"name": "Index", "field": "Doc", "model": "nomicai/nomic-embed-text-v1"}
  ]
);
```
{% endtab %}
{% endtabs %}

## Mistral AI Embedding

Epsilla supports these Mistral AI embedding models (learn more about Mistral AI embedding at [https://docs.mistral.ai/guides/embeddings/](https://docs.mistral.ai/guides/embeddings/)):

| Name                        | Dimensions |
| --------------------------- | ---------- |
| **mistralai/mistral-embed** | 1024       |

When using Mistral AI embedding on Docker, make sure provide the **X-MistralAI-API-Key** header when connecting to the vector database:

{% tabs %}
{% tab title="Python" %}
```python
db = vectordb.Client(
    ...
    headers={
        "X-MistralAI-API-Key": <Your Mistral AI API key here>
    }
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const db = new epsillajs.EpsillaDB({
    ...
    headers: {
        "X-MistralAI-API-Key": <Your Mistral AI API key here>
    }
});
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you are using Epsilla Cloud, make sure to add [Mistral AI integration](integrations/mistral-ai.md) instead of passing the header.
{% endhint %}

And use the embedding model when defining the index:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.create_table(
    ...
    indices=[
        {"name": "Index", "field": "Doc", "model": "mistralai/mistral-embed"}
    ]
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.createTable(
  ...
  [
    {"name": "Index", "field": "Doc", "model": "mistralai/mistral-embed"}
  ]
);
```
{% endtab %}
{% endtabs %}
