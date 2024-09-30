# OpenAI

On Epsilla Cloud, you can enable OpenAI integration by providing your OpenAI API key (we securely manage your keys using AWS KMS):

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-18 at 8.51.21 AM.png" alt=""><figcaption></figcaption></figure>

## Embeddings

Epsilla integrates with OpenAI with the following embedding models:

<table><thead><tr><th width="311">Name</th><th width="171">Dimensions</th><th>Support Dimension Reduction</th></tr></thead><tbody><tr><td><strong>openai/text-embedding-3-large</strong></td><td>3072</td><td>Yes</td></tr><tr><td><strong>openai/text-embedding-3-small</strong></td><td>1536</td><td>Yes</td></tr><tr><td><strong>openai/text-embedding-ada-002</strong></td><td>1536</td><td>No</td></tr></tbody></table>

For Epsilla open source vector db, you just need to add a header in the data ingestion and semantic search queries [like this](../embeddings.md#openai-embedding).

Then you can start using the openai embedding model during vector table schema creation:

<figure><img src="../../.gitbook/assets/Screenshot 2024-01-31 at 12.10.57 PM.png" alt=""><figcaption></figcaption></figure>

For models that support dimension reduction, you can optionally provide a dimensions parameter to reduce the embedding response size:

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-13 at 5.29.51 PM (1).png" alt=""><figcaption></figcaption></figure>
