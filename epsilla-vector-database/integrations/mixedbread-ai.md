# Mixedbread AI

On Epsilla Cloud, you can enable Mixedbread AI integration by providing your Mixedbread AI API key (we securely manage your keys using AWS KMS):

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-13 at 11.21.29 AM.png" alt=""><figcaption></figcaption></figure>

## Embeddings

Epsilla integrates with Mixedbread AI with the following embedding models.

| Name                                   | Dimensions |
| -------------------------------------- | ---------- |
| **mixedbreadai/UAE-Large-V1**          | 1024       |
| **mixedbreadai/bge-large-en-v1.5**     | 1024       |
| **mixedbreadai/gte-large**             | 1024       |
| **mixedbreadai/e5-large-v2**           | 1024       |
| **mixedbreadai/multilingual-e5-large** | 1024       |
| **mixedbreadai/multilingual-e5-base**  | 768        |
| **mixedbreadai/gte-large-zh**          | 1024       |

For Epsilla open source vector db, you just need to add a header in the data ingestion and semantic search queries [like this](../embeddings.md#mixedbread-ai-embedding).

Then you can start using the mixedbreadai embedding model during vector table schema creation:

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-13 at 11.23.10 AM.png" alt=""><figcaption></figcaption></figure>
