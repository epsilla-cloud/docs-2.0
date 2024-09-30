# Delete a database

## Unload a database using Epsilla Docker

You can use this command to unload a database from memory. The database files are still retained on disk.

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.unload_db(db_name="myDB")
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.unloadDB('MyDB');
```
{% endtab %}
{% endtabs %}

## Delete a database on Epsilla Cloud

For now, you can delete vector databases via Cloud GUI.

<figure><img src="../.gitbook/assets/Screenshot 2023-11-22 at 10.38.29 AM.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
We will support deleting databases via Python/JavaScript client in the near future.
{% endhint %}
