# Local Files

**Local Files** data source in Epsilla allows users to upload and manage documents directly from their local storage (like laptop). This type of data source is ideal for adding static content, such as PDFs, Word documents, or spreadsheets, to the knowledge base for retrieval purposes.

### **Select Knowledge Base Type** <a href="#select-knowledge-base-type" id="select-knowledge-base-type"></a>

Choose **Local Files** to continue.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-29 at 11.42.04 PM.png" alt="" width="326"><figcaption></figcaption></figure>

### Knowledge Base Name

Provide a **Knowledge Base Name**. A valid name should start with a letter or '\_', and can contain only letters, digits, underscores, and whitespaces.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-29 at 11.45.11 PM (2).png" alt="" width="563"><figcaption></figcaption></figure>

### **Upload Data** <a href="#upload-data" id="upload-data"></a>

Select the documents you want to use. You can click the file uploader to pick files, or directly drag the files to upload:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 12.00.40 AM.png" alt=""><figcaption></figcaption></figure>

You can inspect the uploaded files in the list.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 12.01.28 AM.png" alt=""><figcaption></figcaption></figure>

For deep customization of the knowledge base, read more at [Advanced Settings](advanced-settings/).

### **Data Processing** <a href="#data-processing" id="data-processing"></a>

Once the data is uploaded, click **Create:**

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 9.57.34 PM.png" alt=""><figcaption></figcaption></figure>

Epsilla Cloud will automatically process the files (under the hood, Epsilla will load the files, chunk them, and embed into vectors. [Read more here](https://blog.epsilla.com/large-scale-smart-etl-for-unstructured-data-in-rag-systems-with-epsilla-7fd86fa8d6cd)), You can monitor the progress of data processing:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 9.57.47 PM.png" alt=""><figcaption></figcaption></figure>

You can inspect the processed data (chunks) at the [**Data Storage**](data-storage.md) tab.
