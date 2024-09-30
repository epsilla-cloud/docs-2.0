# Mistral AI

On Epsilla Cloud, you can enable Mistral AI integration by providing your Mistral AI API key (we securely manage your keys using AWS KMS):

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-13 at 11.22.05 AM.png" alt=""><figcaption></figcaption></figure>

## Embeddings

Epsilla integrates with Nomic AI with the following embedding models.

| Name                        | Dimensions |
| --------------------------- | ---------- |
| **mistralai/mistral-embed** | 1024       |

For Epsilla open source vector db, you just need to add a header in the data ingestion and semantic search queries [like this](../embeddings.md#mistral-ai-embedding).

Then you can start using the nomicai embedding model during vector table schema creation:

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-13 at 11.23.40 AM.png" alt=""><figcaption></figcaption></figure>
