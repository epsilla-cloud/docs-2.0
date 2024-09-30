---
description: Each table can hold multiple records.
---

# Insert records

### Insert records

Make sure the records comply with the defined table schema.

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.insert(
  table_name="MyTable",
  records=[
    {"ID": 1, "Doc": "The garden was blooming with vibrant flowers, attracting butterflies and bees with their sweet nectar.", "Embedding": [0.05, 0.61, 0.76, 0.74]},
    {"ID": 2, "Doc": "In the busy city streets, people rushed to and fro, hardly noticing the beauty of the day.", "Embedding": [0.19, 0.81, 0.75, 0.11]},
    {"ID": 3, "Doc": "The library was a quiet haven, filled with the scent of old books and the soft rustling of pages.", "Embedding": [0.36, 0.55, 0.47, 0.94]},
    {"ID": 4, "Doc": "High in the mountains, the air was crisp and clear, revealing breathtaking views of the valley below.", "Embedding": [0.18, 0.01, 0.85, 0.80]},
    {"ID": 5, "Doc": "At the beach, children played joyfully in the sand, building castles and chasing the waves.", "Embedding": [0.24, 0.18, 0.22, 0.44]}
  ]
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.insert('MyTable',
  [
    {"ID": 1, "Doc": "The garden was blooming with vibrant flowers, attracting butterflies and bees with their sweet nectar.", "Embedding": [0.05, 0.61, 0.76, 0.74]},
    {"ID": 2, "Doc": "In the busy city streets, people rushed to and fro, hardly noticing the beauty of the day.", "Embedding": [0.19, 0.81, 0.75, 0.11]},
    {"ID": 3, "Doc": "The library was a quiet haven, filled with the scent of old books and the soft rustling of pages.", "Embedding": [0.36, 0.55, 0.47, 0.94]},
    {"ID": 4, "Doc": "High in the mountains, the air was crisp and clear, revealing breathtaking views of the valley below.", "Embedding": [0.18, 0.01, 0.85, 0.80]},
    {"ID": 5, "Doc": "At the beach, children played joyfully in the sand, building castles and chasing the waves.", "Embedding": [0.24, 0.18, 0.22, 0.44]}
  ]
);
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Starting from v0.3.3, Epsilla will automatically converting floating numbers as integers during insertion.
{% endhint %}
