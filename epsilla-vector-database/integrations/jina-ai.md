# Jina AI

On Epsilla Cloud, you can enable Jina AI integration by providing your Jina AI API key (we securely manage your keys using AWS KMS):

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-18 at 8.52.08 AM.png" alt=""><figcaption></figcaption></figure>

## Embeddings

Epsilla integrates with Jina AI with the following embedding models.

| Name                                    | Dimensions |
| --------------------------------------- | ---------- |
| **jinaai/jina-embeddings-v2-base-en**   | 768        |
| **jinaai/jina-embeddings-v2-base-de**   | 768        |
| **jinaai/jina-embeddings-v2-base-es**   | 768        |
| **jinaai/jina-embeddings-v2-base-zh**   | 768        |
| **jinaai/jina-embeddings-v2-base-code** | 768        |
| **jinaai/jina-embeddings-v2-small-en**  | 512        |

For Epsilla open source vector db, you just need to add a header in the data ingestion and semantic search queries [like this](../embeddings.md#jina-ai-embedding).

Then you can start using the jinaai embedding model during vector table schema creation:

<figure><img src="../../.gitbook/assets/Screenshot 2024-01-10 at 10.52.40 AM.png" alt=""><figcaption></figcaption></figure>
