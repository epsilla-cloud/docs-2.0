# Voyage AI

On Epsilla Cloud, you can enable Voyage AI integration by providing your Voyage AI API key (we securely manage your keys using AWS KMS):

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-18 at 8.52.45 AM.png" alt=""><figcaption></figcaption></figure>

## Embeddings

Epsilla integrates with Voyage AI with the following embedding models:

### Standard Embedding Models

| Name                                 | Dimensions          | Type     |
| ------------------------------------ | ------------------- | -------- |
| **voyageai/voyage-3.5**              | 1024 (configurable) | Standard |
| **voyageai/voyage-3.5-lite**         | 1024 (configurable) | Standard |
| **voyageai/voyage-3**                | 1024                | Standard |
| **voyageai/voyage-3-lite**           | 512                 | Standard |
| **voyageai/voyage-large-2**          | 1536                | Standard |
| **voyageai/voyage-2**                | 1024                | Standard |
| **voyageai/voyage-code-2**           | 1536                | Standard |
| **voyageai/voyage-lite-02-instruct** | 1024                | Standard |

{% hint style="info" %}
**voyage-3.5** and **voyage-3.5-lite** support configurable dimensions: 2048, 1024 (default), 512, and 256. They also support multiple quantization options (int8, uint8, binary, ubinary) for optimized storage and performance.
{% endhint %}

### Contextualized Embedding Models

Contextualized embeddings capture both local chunk details and global document context for improved retrieval accuracy.

| Name                      | Dimensions          | Features                                   |
| ------------------------- | ------------------- | ------------------------------------------ |
| **voyage-context-3**      | 1024 (configurable) | Context-aware, dimension reduction support |

**Key Features:**
- Captures both local and global context
- Dimension reduction: 256, 512, 1024, 2048
- Output formats: float, int8, uint8, binary, ubinary
- Max 1,000 inputs, 120K tokens, 16K chunks per request

### Multimodal Embedding Models

Multimodal embeddings support text-based content (image support requires additional libraries in self-hosted deployments).

| Name                      | Dimensions | Features                    |
| ------------------------- | ---------- | --------------------------- |
| **voyage-multimodal-3**   | 1024       | Text embeddings, auto-truncate |

**Key Features:**
- Text-only support (image support coming soon)
- Auto-truncation to context length
- Context length: 32,000 tokens
- Max 1,000 inputs, 320K tokens per request

## Automatic API Routing

Epsilla automatically routes to the appropriate Voyage AI API based on the model name you specify:

- Models containing `voyage-context` → Contextualized Embeddings API
- Models containing `voyage-multimodal` → Multimodal Embeddings API
- All other models → Standard Embeddings API

**No code changes needed** - just use the model name that fits your use case!

## Usage

For Epsilla open source vector db, you just need to add a header in the data ingestion and semantic search queries [like this](../embeddings.md#voyage-ai-embedding).

Then you can start using the voyageai embedding models during vector table schema creation:

<figure><img src="../../.gitbook/assets/Screenshot 2024-01-31 at 12.10.07 PM.png" alt=""><figcaption></figcaption></figure>

### Example: Complete Workflow with Standard Embeddings

Here's a complete example showing how to create a table, insert documents, and perform semantic search:

{% tabs %}
{% tab title="Python" %}
```python
from pyepsilla import vectordb

# Connect to Epsilla
client = vectordb.Client(
    protocol='http',
    host='localhost',
    port='8888'
)

# Load database
client.load_db(db_name="MyDB", db_path="/tmp/epsilla")
client.use_db(db_name="MyDB")

# Create table with VoyageAI embeddings
status_code, response = client.db.create_table(
    table_name="KnowledgeBase",
    table_fields=[
        {"name": "ID", "dataType": "INT", "primaryKey": True},
        {"name": "Doc", "dataType": "STRING"}
    ],
    indices=[
        {"name": "DocIndex", "field": "Doc", "model": "voyageai/voyage-3"}
    ]
)

# Insert documents (embeddings generated automatically)
status_code, response = client.db.insert(
    table_name="KnowledgeBase",
    records=[
        {"ID": 1, "Doc": "Artificial intelligence is transforming technology."},
        {"ID": 2, "Doc": "Machine learning enables computers to learn from data."},
        {"ID": 3, "Doc": "Neural networks are inspired by biological neurons."}
    ],
    headers={
        "X-VoyageAI-API-Key": "vo-your-api-key-here"
    }
)

# Semantic search
status_code, response = client.db.query(
    table_name="KnowledgeBase",
    query_field="Doc",
    query_text="What is AI?",
    limit=2,
    headers={
        "X-VoyageAI-API-Key": "vo-your-api-key-here"
    }
)

print("Search results:", response)
# Output shows the most semantically similar documents
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
import { EpsillaDB } from '@epsilla-inc/epsilla-node-client';

// Connect to Epsilla
const client = new EpsillaDB({
  protocol: 'http',
  host: 'localhost',
  port: 8888
});

// Load and use database
await client.loadDB('MyDB', '/tmp/epsilla');
await client.useDB('MyDB');

// Create table with VoyageAI embeddings
await client.createTable('KnowledgeBase',
  [
    {"name": "ID", "dataType": "INT", "primaryKey": true},
    {"name": "Doc", "dataType": "STRING"}
  ],
  [
    {"name": "DocIndex", "field": "Doc", "model": "voyageai/voyage-3"}
  ]
);

// Insert documents (embeddings generated automatically)
await client.insert('KnowledgeBase',
  [
    {"ID": 1, "Doc": "Artificial intelligence is transforming technology."},
    {"ID": 2, "Doc": "Machine learning enables computers to learn from data."},
    {"ID": 3, "Doc": "Neural networks are inspired by biological neurons."}
  ],
  {
    headers: {
      "X-VoyageAI-API-Key": "vo-your-api-key-here"
    }
  }
);

// Semantic search
const results = await client.query('KnowledgeBase', {
  queryField: 'Doc',
  queryText: 'What is AI?',
  limit: 2,
  headers: {
    "X-VoyageAI-API-Key": "vo-your-api-key-here"
  }
});

console.log('Search results:', results);
// Output shows the most semantically similar documents
```
{% endtab %}
{% endtabs %}

### Example: Using Contextualized Embeddings

```python
# Create table with contextualized embeddings
status_code, response = db.create_table(
    table_name="MyContextualTable",
    table_fields=[
        {"name": "ID", "dataType": "INT", "primaryKey": True},
        {"name": "Doc", "dataType": "STRING"}
    ],
    indices=[
        {"name": "Index", "field": "Doc", "model": "voyage-context-3"}
    ]
)
```

### Example: Using Multimodal Embeddings

```python
# Create table with multimodal embeddings (text-only)
status_code, response = db.create_table(
    table_name="MyMultimodalTable",
    table_fields=[
        {"name": "ID", "dataType": "INT", "primaryKey": True},
        {"name": "Doc", "dataType": "STRING"}
    ],
    indices=[
        {"name": "Index", "field": "Doc", "model": "voyage-multimodal-3"}
    ]
)
```

## Learn More

- [VoyageAI Contextualized Embeddings Documentation](https://docs.voyageai.com/docs/contextualized-chunk-embeddings)
- [VoyageAI Multimodal Embeddings Documentation](https://docs.voyageai.com/docs/multimodal-embeddings)
- [VoyageAI API Reference](https://docs.voyageai.com/reference)
