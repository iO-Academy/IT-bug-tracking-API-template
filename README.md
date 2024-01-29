# IT-bug-tracking-API-template

# API documentation

### Return all issues

* **URL**

  /issues.php

* **Method:**

  `GET`

* **URL Params**

  **Required:**

  There are no required URL params

  **Optional:**
  
  `tag=[string]` - filters issues by tag
  `severity=[comma seperated ids]` - filters issues by severity
  `order=[string]` - orders returned issues, options: `oldest`, `severity`, `comments`. Defaults to most recent first when left blank
  
* **Success Response:**

    * **Code:** 200 <br />
      **Content:** <br />

```json
{
  "issues": [
    {
      "id": 1,
      "title": "Title of the ticket",
      "severity": "Moderate",
      "tags": ["tag 1", "tag 2", "tag 3"],
      "date_created": "01/05/2023",
      "comment_count": 3
      
    },
    {
      "id": 2,
      "title": "Title of the ticket",
      "severity": "Low",
      "tags": ["tag 1", "tag 2", "tag 3"],
      "date_created": "01/05/2023",
      "comment_count": 12
    }
  ]
}
```

* **Error Response:**

  * **Code:** 400 BAD REQUEST <br />
    **Content:** `{"message": "Unknown tag filter"}`

  * **Code:** 400 BAD REQUEST <br />
    **Content:** `{"message": "Unknown severity filter"}`

  * **Code:** 400 BAD REQUEST <br />
    **Content:** `{"message": "Unknown order parameter"}`

  * **Code:** 500 SERVER ERROR <br />
    **Content:** `{"message": "Unexpected error"}`
