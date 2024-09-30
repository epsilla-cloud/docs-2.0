# Voyage AI

On Epsilla Cloud, you can enable Voyage AI integration by providing your Voyage AI API key (we securely manage your keys using AWS KMS):

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-18 at 8.52.45 AM.png" alt=""><figcaption></figcaption></figure>

## Embeddings

Epsilla integrates with Voyage AI with the following embedding models:

| Name                                 | Dimensions |
| ------------------------------------ | ---------- |
| **voyageai/voyage-3**                | 1024       |
| **voyageai/voyage-3-lite**           | 512        |
| **voyageai/voyage-large-2**          | 1536       |
| **voyageai/voyage-2**                | 1024       |
| **voyageai/voyage-code-2**           | 1536       |
| **voyageai/voyage-lite-02-instruct** | 1024       |

For Epsilla open source vector db, you just need to add a header in the data ingestion and semantic search queries [like this](../embeddings.md#voyage-ai-embedding).

Then you can start using the voyageai embedding models during vector table schema creation:

<figure><img src="../../.gitbook/assets/Screenshot 2024-01-31 at 12.10.07 PM.png" alt=""><figcaption></figcaption></figure>
