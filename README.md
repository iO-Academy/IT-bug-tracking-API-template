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
  
  * `completed=[0 or 1]` - filters issues by completion
  * `severity=[comma seperated ints]` - filters issues by severity  
  * `order=string` - orders returned issues, options: `oldest`, `severity`, `comments`. Defaults to most recent first when left blank  
  
* **Success Response:**

    * **Code:** 200 <br />
      **Content:** <br />

```json
{
  "issues": [
    {
      "id": 1,
      "title": "Title of the ticket",
      "summary": "first 100 characters of issue description",
      "severity": "Moderate",
      "date_created": "01/05/2023",
      "comment_count": 3,
      "completed": false
    },
    {
      "id": 2,
      "title": "Title of the ticket",
      "summary": "first 100 characters of issue description",
      "severity": "Low",
      "date_created": "01/05/2023",
      "comment_count": 12,
      "completed": true
    }
  ]
}
```

* **Error Response:**

  * **Code:** 400 BAD REQUEST <br />
    **Content:** `{"message": "Unknown severity filter"}`

  * **Code:** 400 BAD REQUEST <br />
    **Content:** `{"message": "Unknown order parameter"}`

  * **Code:** 500 SERVER ERROR <br />
    **Content:** `{"message": "Unexpected error"}`

### Return a single issue

* **URL**

  /issue.php

* **Method:**

  `GET`

* **URL Params**

  **Required:**

  `id=int` - id of the issue to return

  **Optional:**
  
  There are no optional URL params
  
* **Success Response:**

    * **Code:** 200 <br />
      **Content:** <br />

```json
{
  "id": 1,
  "title": "Title of the ticket",
  "severity": "Moderate",
  "date_created": "01/05/2023",
  "comment_count": 3,
  "reporter": "Sarah Dunkin",
  "department": 1,
  "description": "Bombay. Tabby tiger american bobtail cornish rex. Ocicat tom kitten cougar. Donskoy tomcat russian blue yet sphynx.",
  "comments": [
    {
      "name": "Amy Robinson",
      "comment": "Lorum ipsum delor vadot",
      "date_created": "01/05/2023 13:00"
    },
    {
      "name": "Amy Robinson",
      "comment": "Lorum ipsum delor vadot",
      "date_created": "01/05/2023 13:02"
    }
  ]
}
```

* **Error Response:**

  * **Code:** 400 BAD REQUEST <br />
    **Content:** `{"message": "Unknown issue id"}`

  * **Code:** 500 SERVER ERROR <br />
    **Content:** `{"message": "Unexpected error"}`

### Return all severities

* **URL**

  /severities.php

* **Method:**

  `GET`

* **URL Params**

  **Required:**

  There are no optional URL params

  **Optional:**
  
  There are no optional URL params
  
* **Success Response:**

    * **Code:** 200 <br />
      **Content:** <br />

```json
{
  "severities": [
    {
      "name": "Critical",
      "id": 1
    },
    {
      "name": "Severe",
      "id": 2
    }
  ]
}
```

* **Error Response:**

  * **Code:** 500 SERVER ERROR <br />
    **Content:** `{"message": "Unexpected error"}`
    

### Create a new issue

* **URL**

  /report.php

* **Method:**

  `POST`

* **URL Params**

  **Required:**

  There are no required URL params

  **Optional:**
  
  There are no optional URL params

* **Body Data**

  **Required**: <br />
  ```json
  {
    "name": "String",
    "department": int,
    "title": "String",
    "description": "String",
    "severity": int
  }
  ```
  
* **Success Response:**

    * **Code:** 201 <br />
      **Content:** <br />

```json
{"message": "Issue created", "id": int}
```

* **Error Response:**

  * **Code:** 400 BAD REQUEST <br />
    **Content:** `{"message": "Invalid issue data"}`

  * **Code:** 500 SERVER ERROR <br />
    **Content:** `{"message": "Unexpected error"}`


### Add a new comment

* **URL**

  /comment.php

* **Method:**

  `POST`

* **URL Params**

  **Required:**

  `id=int` - id of the issue to add a comment to

  **Optional:**
  
  There are no optional URL params

* **Body Data**

  **Required**: <br />
  ```json
  {
    "name": "String",
    "comment": "String"
  }
  ```
  
* **Success Response:**

    * **Code:** 201 <br />
      **Content:** <br />

```json
{"message": "Comment added", "id": int}
```

* **Error Response:**

  * **Code:** 400 BAD REQUEST <br />
    **Content:** `{"message": "Invalid comment data"}`

  * **Code:** 500 SERVER ERROR <br />
    **Content:** `{"message": "Unexpected error"}`


### Mark an issue as complete

* **URL**

  /complete.php

* **Method:**

  `GET`

* **URL Params**

  **Required:**

  `id=string` - id of the issue to mark as complete

  **Optional:**
  
  No optional URL params
  
* **Success Response:**

    * **Code:** 200 <br />
      **Content:** <br />

```json
{"message": "Issue <ID> has been completed"}
```

* **Error Response:**

  * **Code:** 400 BAD REQUEST <br />
    **Content:** `{"message": "Missing issue id"}`

  * **Code:** 400 BAD REQUEST <br />
    **Content:** `{"message": "Unknown issue id"}`

  * **Code:** 500 SERVER ERROR <br />
    **Content:** `{"message": "Unexpected error"}`
