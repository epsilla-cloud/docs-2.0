# Nomic AI

On Epsilla Cloud, you can enable Nomic AI integration by providing your Nomic AI API key (we securely manage your keys using AWS KMS):

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-13 at 11.21.53 AM.png" alt=""><figcaption></figcaption></figure>

## Embeddings

Epsilla integrates with Nomic AI with the following embedding models.

<table><thead><tr><th width="322">Name</th><th width="133">Dimensions</th><th>Support Dimension Reduction</th></tr></thead><tbody><tr><td><strong>nomicai/nomic-embed-text-v1.5</strong></td><td>768</td><td>Yes</td></tr><tr><td><strong>nomicai/nomic-embed-text-v1</strong></td><td>768</td><td>No</td></tr></tbody></table>

For Epsilla open source vector db, you just need to add a header in the data ingestion and semantic search queries [like this](../embeddings.md#nomic-ai-embedding).

Then you can start using the nomicai embedding model during vector table schema creation:

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-13 at 11.23.30 AM.png" alt=""><figcaption></figcaption></figure>

For models that support dimension reduction, you can optionally provide a dimensions parameter to reduce the embedding response size:

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-14 at 4.23.37 PM.png" alt=""><figcaption></figcaption></figure>
