# Retrieve records (with filters and pagination)

Epsilla supports the retrieval of records from a table. By default, it retrieves all records from the table. Users can provide a primary key list to specify which records to retrieve; users can provide a filter condition to constrain the records obtained; users can provide 'limit' and 'skip' parameters to implement pagination on the records being retrieved.

Below is the complete example for all supported parameters:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.get(
  table_name="MyTable",                  # The name of the table to query against.
  response_fields=["Doc"],               # (Optional) which fields to be included in
                                         # the response. If not provided, will include
                                         # all fields in the table.
  primary_keys=[1, 2, 4, 5],             # (Optional) the list of primary keys for retrieval.
                                         # If not provided, will not constrian on primary key
                                         # value.
  filter="Doc <> 'London'",              # (Optional) a boolean expression for filtering
                                         # out the results.
  skip=0,                                # (Optional) how many records to skip. If not
                                         # provided, will not skip any records.
  limit=2                                # (Optional) how many records to retrieve. If not
                                         # provided, will return all records (after the
                                         # skipped ones)
)
print(response)
```

Response example:

```
{'statusCode': 200, 'message': 'Query get successfully.', 'result': [{'Doc': 'Berlin'}, {'Doc': 'San Francisco'}]}
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const query = await db.get(
  'MyTable',                                 // The name of the table to query against.
  {
    response: ["Doc"],                       // (Optional) which fields to be included in
                                             // the response. If not provided, will include
                                             // all fields in the table.
    primaryKeys: [1, 2, 4, 5],               // (Optional) the list of primary keys for retrieval.
                                             // If not provided, will not constrian on primary key
                                             // value.
    filter: 'ID < 6 AND Doc <> \'London\'',  // (Optional) filter: a boolean expression for filtering
                                             // out the results.
    skip: 0,                                 // (Optional) how many records to skip. If not
                                             // provided, will not skip any records.
    limit: 2                                 // (Optional) how many records to retrieve. If not
                                             // provided, will return all records (after the
                                             // skipped ones)
  }
);
console.log(JSON.stringify(query, undefined, 2));
```

Response example:

```
{
  "statusCode": 200,
  "message": "Query get successfully.",
  "result": [
    {
      "Doc": "Moscow"
    },
    {
      "Doc": "San Francisco"
    }
  ]
}
```
{% endtab %}
{% endtabs %}

And below is the example with minimum parameters for retrieving records:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.get(
  table_name="MyTable",
  limit=2
)
print(response)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const query = await db.get(
  'MyTable',
  {
      limit: 2
  }
);
console.log(JSON.stringify(query, undefined, 2));
```
{% endtab %}
{% endtabs %}
