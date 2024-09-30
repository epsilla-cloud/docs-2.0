# Data Storage

Data storage in Epsilla manages the underlying stored data records (chunks) from the knowledge base. Users can perform CRUD (Create, Read, Update, Delete) operations on these records, manage tables, and inspect the details of each record. Additionally, users can view the table schema to understand the structure and organization of stored data.

### **Inspect Data** <a href="#inspect-data" id="inspect-data"></a>

If you are create a knowledge base from any data source type other than **Basic** (which means creating knowledge base from scratch), the `knowledge_table` will already be automatically . You can inspect the processed data (chunks). By default, the first 20 chunks will be visualized when you enter the tab:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.03.01 PM.png" alt=""><figcaption></figcaption></figure>

Click a record to inspect the data detail:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.03.18 PM.png" alt=""><figcaption></figcaption></figure>

By default, each record in Epsilla's knowledge base contains the following fields:

* **ID**: A unique UUID to distinguish each record in the knowledge base.
* **Content**: The chunk content as a string.
* **Filename**: The file's name, the webpage's URL, or the identifier in the data source.
* **Timestamp**: The epoch time (in milliseconds) when the record was loaded or updated.
* **Metadata**: Additional information about the chunk, such as `DataSourceType` (e.g., file), `FileType` (e.g., pdf), and `Pages` (a list indicating the pages where this chunk is located, starting at page 1). Note that this metadata differs from the "Meta Data" configured in Advanced Settings.

If Meta Data is configured, additional fields mapped from that meta data will also be shown in the record details.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 12.34.55 AM.png" alt="" width="375"><figcaption></figcaption></figure>

Use the **Records per page** setting to adjust how many records are displayed in each batch.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 12.39.23 AM.png" alt="" width="115"><figcaption></figcaption></figure>

You can navigate between batches using the **Prev** and **Next** buttons to scroll through the records.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 12.39.29 AM.png" alt="" width="184"><figcaption></figcaption></figure>

### Semantic Search

You can enter a natural language query in the search box to find the top K most relevant records based on meaning rather than exact keywords; this is known as semantic search.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 12.51.57 AM.png" alt=""><figcaption></figcaption></figure>

Click the settings button to open the advanced search setup. By default, the **Content** field is semantically indexed by **Index**. If you have added other semantic indexes to the table, you can select a different index for searching.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 12.55.05 AM.png" alt="" width="242"><figcaption></figcaption></figure>

You can also specify a filter expression for the search:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 12.58.42 AM.png" alt="" width="244"><figcaption></figcaption></figure>

It will be applied along with the semantic search to further narrow down the results.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 12.59.02 AM.png" alt=""><figcaption></figcaption></figure>

Read more about supported [filter expression](../epsilla-vector-database/search-the-top-k-semantically-similar-records.md#filter-expression).

### Add New Records

Click the Add New Record button at bottom right corner:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 1.02.32 AM.png" alt="" width="76"><figcaption></figcaption></figure>

And you can insert new records to the knowledge base (following the table schema):

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 1.03.53 AM.png" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="info" %}
It is recommended to use the data source's automatic processing of records instead of manually inserting records.
{% endhint %}

### Delete Records

Hover over a record with your mouse, then click the **Trash Can** icon to delete it.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 1.07.45 AM.png" alt="" width="314"><figcaption></figcaption></figure>

Confirm Delete:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 1.07.50 AM.png" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="info" %}
Deleting records is irreversible. It is recommended to rely on the data source's automatic processing of records rather than manually deleting them.
{% endhint %}

### Inspect Table Information

Hover over a table with your mouse, then click the **Edit** icon to view and inspect the table information.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 1.22.07 AM.png" alt="" width="326"><figcaption></figcaption></figure>

The first tab displays the table schema, which defines the structure of the table, including the fields, data types, and semantic indices. Read more about [table schema](../epsilla-vector-database/create-a-new-table.md#create-a-table-on-epsilla-cloud-portal-ui).

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 1.22.54 AM.png" alt="" width="563"><figcaption></figcaption></figure>

The second tab displays the APIs that can be used to programmatically manipulate data in the table, allowing for operations such as creating, reading, updating, and deleting records through code:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 1.24.12 AM.png" alt="" width="563"><figcaption></figcaption></figure>

For each API, three implementation methods are provided: **cURL**, **Python**, and **JavaScript**, allowing users to choose their preferred language or tool for interacting with the table data programmatically:

<div>

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 1.24.45 AM.png" alt=""><figcaption><p>cURL</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 1.25.10 AM.png" alt=""><figcaption><p>Python</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 1.25.18 AM.png" alt=""><figcaption><p>JavaScript</p></figcaption></figure>

</div>

### Create New Table

If you want to define your own knowledge schema, particularly when building from scratch using a **Basic** type knowledge base, click the **Create Table** button to create a new table:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 1.34.37 AM.png" alt="" width="128"><figcaption></figcaption></figure>

The table fields at the "Create Table" stage define the structure and type of data each column will store. You can specify the field names, data types (such as string, integer, or boolean), and any constraints (e.g., Primary Key) to ensure the data is organized correctly and adheres to the intended format:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 1.34.30 AM.png" alt="" width="563"><figcaption></figcaption></figure>

Read more about the table fields at [create table](../epsilla-vector-database/create-a-new-table.md#create-a-table-on-epsilla-cloud-portal-ui).

### Delete Table

Hover over a table with your mouse, then click the **Trash Can** icon to delete the table.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 1.39.22 AM.png" alt="" width="257"><figcaption></figcaption></figure>

Confirm Delete:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-30 at 1.34.08 AM.png" alt="" width="375"><figcaption></figcaption></figure>
