---
title: "Nuclino API Authentication"
---

20-Nov-24

The Nuclino API has an unusual format for authentication.

See the authentication docs [here](https://help.nuclino.com/8090bb76-authentication).

## CURL authentication

Example:

```bash
curl https://api.nuclino.com/v0/teams \
-H "Authorization: YOUR_API_KEY"
```

## Functional Python call to create a note at the items endpoint

```python
def create_nuclino_note(title, content):
    url = "https://api.nuclino.com/v0/items"
    headers = {
        "Authorization": f"{NUCLINO_API_KEY}",   
        "Content-Type": "application/json"
    }
```