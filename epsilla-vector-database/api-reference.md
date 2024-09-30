# Drop a table

## Drop a table from a database in code&#x20;

In both self-hosted Epsilla and Epsilla Cloud, you can use the following code to programmatically drop tables:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.drop_table(table_name="MyTable")
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.dropTable('MyTable');
```
{% endtab %}
{% endtabs %}

## Drop a table on Epsilla Cloud portal UI

On Epsilla Cloud, you can also intuitively drop vector tables via GUI

<figure><img src="../.gitbook/assets/Screenshot 2023-11-22 at 12.27.54 AM (1).png" alt=""><figcaption></figcaption></figure>
