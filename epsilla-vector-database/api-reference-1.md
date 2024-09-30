# Delete records

Delete records with primary keys:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.delete(
  table_name="MyTable",        # The name of the table to delete records against.
  primary_keys=[1, 2, 5]       # The primary keys of the records to be deleted.
)
print(response)
```

Response example:

```
{'statusCode': 200, 'message': 'Delete data from MyTable successfully.', 'result': {'deleted': 3}}
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const query = await db.delete(
  'MyTable',                  // The name of the table to delete records against.
  {
    primaryKeys: [1, 2, 5]    // The primary keys of the records to be deleted.
  }
);
console.log(JSON.stringify(query, undefined, 2));
```

Response example:

```
{
  "statusCode": 200,
  "message": "Delete data from MyTable successfully.",
  "result": {
    "deleted": 3
  }
}
```
{% endtab %}
{% endtabs %}

Delete all records that satisfy a filter condition:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.delete(
  table_name="MyTable",                 # The name of the table to delete records against.
  filter="ID < 6 AND Doc <> 'London'",  # (Optional) a boolean expression for specifying
                                        # which records to be deleted.
)
print(response)
```

Response example:

```
{'statusCode': 200, 'message': 'Delete data from MyTable successfully.', 'result': {'deleted': 14}}
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const query = await db.delete(
  'MyTable',                                 // The name of the table to delete records against.
  {
    filter: 'ID < 6 AND Doc <> \'London\''   // (Optional) a boolean expression for specifying
                                             // which records to be deleted.
  }
);
console.log(JSON.stringify(query, undefined, 2));
```

Response example:

```
{
  "statusCode": 200,
  "message": "Delete data from MyTable successfully.",
  "result": {
    "deleted": 14
  }
}
```
{% endtab %}
{% endtabs %}
