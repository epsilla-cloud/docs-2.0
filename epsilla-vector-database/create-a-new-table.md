---
description: >-
  In Epsilla, you can have multiple tables in a database. A table has its name,
  and multiple fields. Each field has its name, data type, and specific
  configurations.
---

# Create a new table

## Create a table in code

In both self-hosted Epsilla and Epsilla Cloud, you can use the following code to programmatically create tables:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.create_table(
    table_name="MyTable",
    table_fields=[
        {"name": "ID", "dataType": "INT", "primaryKey": True},
        {"name": "Doc", "dataType": "STRING"},
        {"name": "Embedding", "dataType": "VECTOR_FLOAT", "dimensions": 4}
    ],
    # Optionally, add indices on STRING fields with automatic embedding and indexing
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
    {"name": "Doc", "dataType": "STRING"},
    {"name": "Embedding", "dataType": "VECTOR_FLOAT", "dimensions": 4}
  ],
  // Optionally, add indices on STRING fields with automatic embedding and indexing
  [
    {"name": "Index", "field": "Doc", "model": "BAAI/bge-small-en-v1.5"}
  ]
);
```
{% endtab %}
{% endtabs %}

## Create a table on Epsilla Cloud portal UI

On Epsilla Cloud, you can also intuitively create vector tables via GUI. Use the 'Add Field' button to add more fields; Use the 'Add Index' button to add more embedding indices;  Use the 'Delete' buttons to remove a field or index; Give each field a name, data type, and additional options; Choose the desired embedding model for each index.

<figure><img src="../.gitbook/assets/Screenshot 2023-12-28 at 10.02.27 PM.png" alt=""><figcaption></figcaption></figure>

## Field Data Types

We can define different data types for each field. Here are supported data types:

```
TINYINT      # An int with value range [-256, 255]
SMALLINT     # An int with value range [-65536, 65535]
INT          # An int with value range [-2147483648, 2147483647]
BIGINT       # An int with value range [-9223372036854775808, 9223372036854775807]
FLOAT        # A float field
DOUBLE       # A double field
STRING       # A string field
BOOL         # A boolean field
JSON         # Any valid JSON
VECTOR_FLOAT # A vector of float field, dimension must be provided
SPARSE_VECTOR_FLOAT # A sparse vector of float, dimension must be provided
```

Learning more about [dense vector vs. sparse vector](dense-vector-vs.-sparse-vector.md).

### Embedding Fields

Epsilla supports defining multiple embedding fields in one table. This is very convenient for you to bring in your own embeddings, and manage multiple embeddings (could be embedded from different models) for the same documents.&#x20;

For an embedding field, you need to provide a dimension parameter, which specifies how many numbers are stored in each vector. This number needs to be consistent with the embedding model that you are using to embed the raw data.

### Metric Type

When you specify an embedding field, you can also designate a metric type for the embedding model. The metric types supported currently are **Euclidean**, **Cosine**, and **Dot Product**. Here’s a brief on the benefits of each metric type:

{% tabs %}
{% tab title="Python" %}
```python
...
    table_fields=[
        ...
        {
            "name": "Embedding",
            "dataType": "VECTOR_FLOAT",
            "dimensions": 4,
            "metricType": "COSINE" # EUCLIDEAN, COSINE, or DOT_PRODUCT
        }
    ]
...
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
...
  [
    ...
    {
      "name": "Embedding",
      "dataType": "VECTOR_FLOAT",
      "dimensions": 4,
      "metricType": "COSINE" // EUCLIDEAN, COSINE, or DOT_PRODUCT
    }
  ]
...
```
{% endtab %}
{% endtabs %}

#### **Euclidean Distance**:

* **Intuitive**: The Euclidean distance is straightforward and intuitive as it's the "ordinary" straight-line distance between two points in space. This can be beneficial in applications where interpretability is important.
* **Geometry Preserving**: It preserves the geometric structure of the data, making it suitable for applications where the geometric relationships between data points are significant.

#### **Cosine Distance**:

* **Angle-Based Similarity**: Cosine similarity measures the cosine of the angle between two non-zero vectors. This is particularly useful in scenarios where the angle between vectors is more important than their absolute magnitudes. For instance, in text analysis, cosine similarity can capture the orientation of documents in the vector space irrespective of their length.
* **Normalization**: Cosine similarity inherently accounts for magnitude, making it useful in scenarios where data is normalized or needs to be comparable on a similar scale. Note: when using Cosine metric for embedding field, Epsilla will automatically normalize the vector (i.e., rescale the vector length to 1.0) before storing it.
* At Epsilla, we opt for calculating the Cosine Distance rather than Cosine Similarity. Cosine Distance is defined as 1 - CosineSimilarity, and its values fall within the range of \[0, 2]. A Cosine Distance of 0 indicates that the two vectors are identical, signifying complete similarity. Conversely, a value of 1 implies that the vectors are uncorrelated, bearing no linear relationship. Lastly, a Cosine Distance of 2 denotes that the vectors are diametrically opposite, representing the highest degree of dissimilarity.

**Dot Product**

* **Magnitude and Direction Representation:** The dot product of two vectors captures both their magnitude and direction, offering a comprehensive measure of their similarity. This makes it particularly useful in contexts where both aspects are crucial, such as in certain neural network applications.
* **Unbounded Range:** Unlike cosine similarity or distance, the dot product is not confined to a specific range. It can yield any real number, which can provide a more nuanced understanding of vector relationships but may also require additional processing for interpretation.
* At Epsilla, to enhance the ease of comparing distances when utilizing the dot product metric, we **negate** the values.

In Epsilla, if the metric type is not specified, the system defaults to using the Euclidean metric. This setting may be more suitable for general-purpose embedding applications, while the Cosine metric might be more appropriate for specialized or domain-specific applications.

### Primary Key

Optionally, you can define one field of a table as the primary key. By defining primary key, Epsilla will automatically conduct duplication check, and reject records that have a primary key value that already exists in the table. The primary key field has to be one of the following data types:

```
TINYINT
SMALLINT
INT
BIGINT
STRING
```

## Indices

In addition to bringing in your own embedding results of the documents, Epsilla vector database also supports automatically embed your documents, and index them for fast retrieval. Note: adding indices is optional. You can choose to bring in your own embeddings, or let Epsilla handle embedding for you. However, you need make sure each table contains at least one vector field, or one index.

Define indices as a list. Each index contains 3 parts:

* **name:** the name of the index. It must be unique, and cannot be the same as any field name.
* **field:** the name of the field that will be embedded and indexed by the index. The field must be STRING data type.
* **model (optional):** the embedding model name. If omitted, Epsilla will use the default embedding model **BAAI/bge-small-en-v1.5**. Learn more about supported embedding models [here](embeddings.md).
* **dimensions (optional):** for embedding models that support [dimensionality reduction](https://en.wikipedia.org/wiki/Dimensionality\_reduction), you can provide a dimensions parameter for reducing the embedding dimensions returned by the embedding provider, which can save cost while still preserve a high performance. For example, if the embedding model original dimension is 1536, then you can provide a dimensions value between 1 and 1536 for reduce the dimensions. We don't recommend go below 128 in practice, otherwise the embedding performance will be dramatically lower. The [embeddings page](embeddings.md) shows all embedding models that support dimension reduction.

You can index multiple STRING fields. You can define multiple indices on the same field with different embedding models. This level of flexibility enables hybrid search on the same vector table.

Epsilla normalizes the embedding vectors, and uses Cosine distance as the metric for semantic search.
