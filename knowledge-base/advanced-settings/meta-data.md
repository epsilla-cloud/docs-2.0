# Meta Data

**Meta Data** can enrich the knowledge base records (chunks) with additional information such as content type, author, creation date, or custom tags that align with your business requirements. Adding meta data enhances the quality of semantic search, as it allows for more specific filtering and sorting based on attributes beyond just the content itself. This ultimately improves search relevance, optimizes the retrieval process, and provides richer insights by leveraging the added context of each data record.

Currently, the following data source types support Meta Data:&#x20;

* Local Files
* S3
* Share Point

### Meta Data File Preparation

For each file named `filename.<extension>`, you need to prepare an additional file named `filename_<extension>.meta`. For example, if you have a file `MyFile.pdf`, then you need to prepare its meta data file `MyFile_pdf.meta`.

{% hint style="info" %}
If you decide to use meta data, then you need to prepare a separate meta data file for EACH file. The files that don't have an attached meta data file will be failed to process.
{% endhint %}

The meta file content will be a JSON object, with each field representing a piece of supplementary meta data related to the original file. Here is an example meta data file content:

```json
// MyFile_pdf.meta
{
    "Title": "My File's Title",
    "Author": "Paul Smith",
    "Citation Weight": 5.5
}
```

{% hint style="info" %}
Epsilla doesn't support NULL, and the knowledge table is strong schema. So all meta data files in the same knowledge base should follow the same JSON structure.
{% endhint %}

### Upload Meta Data Files

For **Local File** data source, upload all meta data files together with their original files.

For **S3** and **SharePoint** data source, put the meta data files beside their original files in the bucket or folder.

### Configuration

<figure><img src="../../.gitbook/assets/Screenshot 2024-09-30 at 2.17.29 AM (1).png" alt="" width="563"><figcaption></figcaption></figure>

For Meta File Pattern, use `*.meta`

<figure><img src="../../.gitbook/assets/Screenshot 2024-09-30 at 2.11.38 AM.png" alt="" width="563"><figcaption></figcaption></figure>

For **Meta Fields Schema**, add a field mapping for each field in the JSON object that you want to include in the loaded record. The **Source Name** represents the property name in the JSON object, while the **Field Name** is the name you want to use in the knowledge table. Use the dropdown to specify the data type for each field, ensuring that the information is properly structured and integrated into the knowledge base:

<figure><img src="../../.gitbook/assets/Screenshot 2024-09-30 at 2.12.32 AM.png" alt="" width="563"><figcaption></figcaption></figure>

Here is the possible mapping for the example above:

<figure><img src="../../.gitbook/assets/Screenshot 2024-09-30 at 2.23.36 AM.png" alt="" width="563"><figcaption></figcaption></figure>

To inspect if the meta data is loaded correctly, read more at [Inspect Data](../data-storage.md#inspect-data).
