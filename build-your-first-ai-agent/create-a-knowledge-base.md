# Create a Knowledge Base

A knowledge base is a centralized repository of information used to store, organize, and manage content in a structured and accessible manner. In the context of Epsilla Cloud, it serves as the foundational data source that powers AI-driven applications, such as chatbots and start search agents. A knowledge base can include documents, articles, PDFs, or any relevant files that contain information an AI system can reference to provide accurate and grounded responses. A knowledge base enhances the AI's ability to deliver precise and contextual answers, significantly improving personalization and reducing hallucinations.

### **Access the Knowledge Bases Tab**

On the navigation bar, click on the **Knowledge Bases** tab.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 9.48.53 PM.png" alt="" width="253"><figcaption></figcaption></figure>

This will lead you to the page where you can create and manage all your knowledge bases.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 9.50.29 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### **Click "Create Knowledge Base"**

Locate and click the **Create Knowledge Base** button. This will initiate the setup process for a new knowledge base.

### **Select Knowledge Base Type**

Choose the type of data source you'd like to use for your knowledge base. Epsilla Cloud supports several types, including:

* **Local Files** (e.g., PDFs, Word documents)
* **Websites**
* **Cloud Storage** (e.g., Google Drive, Dropbox, SharePoint, S3)
* **Note-Taking Apps** (e.g., Notion)

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 9.51.56 PM.png" alt=""><figcaption></figcaption></figure>

Here we choose **Local Files**.&#x20;

### Knowledge Base Name

Provide a **Knowledge Base Name**.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-29 at 11.45.11 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### **Upload Data**

Select the documents you want to use. You can click the file uploader to pick files, or directly drag the files to upload:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 9.56.51 PM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 9.57.11 PM.png" alt=""><figcaption></figcaption></figure>

### **Data Processing**

Once the data is uploaded, click **Create:**

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 9.57.34 PM.png" alt=""><figcaption></figcaption></figure>

Epsilla Cloud will automatically process the files (under the hood, Epsilla will load the files, chunk them, and embed into vectors. [Read more here](https://blog.epsilla.com/large-scale-smart-etl-for-unstructured-data-in-rag-systems-with-epsilla-7fd86fa8d6cd)),  You can monitor the progress of data processing:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 9.57.47 PM.png" alt=""><figcaption></figcaption></figure>

### **Inspect Data**

You can inspect the processed data (chunks) at the **Data Storage** tab. By default, the first 20 chunks will be visualized:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.03.01 PM.png" alt=""><figcaption></figcaption></figure>

Click a chunk to inspect the chunk data detail:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.03.18 PM.png" alt=""><figcaption></figcaption></figure>

Read more about inspecting data at [Data Storage](../knowledge-base/data-storage.md).
