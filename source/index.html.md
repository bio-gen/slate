---
title: Healthnet API

language_tabs:
  - http
  - shell: cURL

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: false
---

# Introduction

Welcome to the Healthnet API.

# Registration

```http
POST /v1/users HTTP/1.1
Host: healthnetz.herokuapp.com
Accept: application/vnd
Content-Type: application/vnd.api+json

{
	"data": {
		"type": "users",
	  "attributes": {
	    "email": "brucelee@test.com",
	    "password": "12345678",
	    "password_confirmation": "12345678"
		}
	}
}
```
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "data": {
    "id": "3",
    "type": "users",
    "attributes": {
      "email": "brucelee@test.com",
      "password": "12345678"
    }
  }
}
```

```shell
curl http://healthnetz.herokuapp.com/v1/users
  -X POST
  -H "Accept: application/vnd"
  -H "Content-Type: application/x-www-form-urlencoded"
  -d '{
	"data": {
		"type": "users",
	  "attributes": {
	    "email": "brucelee@test.com",
	    "password": "12345678",
	    "password_confirmation": "12345678"
  	}
  }
}'
```

To authenticate to the API, a user must be registered first.

### HTTP Request

`POST http://healthnetz.herokuapp.com/v1/users`

### Arguments

Parameter | Required | Description
--------- | ------- | -----------
type | Yes | JSON-API data type
email | Yes | Registered user's e-mail address.
password | Yes | Registered user's password
password_confirmation | Yes | Password confirmation
first_name | Yes | User's first name
last_name | Yes | User's last name

# Authentication

```http
POST /v1/auth HTTP/1.1
Host: healthnetz.herokuapp.com
Content-Type: application/json

{
	"auth": {
		"email": "test@test.com",
		"password": "12345678"
	}
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "jwt": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE0OTM3MTc5NDAsInN1YiI6MX0.HFLagVTraZX3y5eiK2YvvzvF4kj0P0aAVYYMoASaCCg"
}
```

```shell
curl http://healthnetz.herokuapp.com/v1/auth
  -X POST
  -d '{
	"auth": {
		"email": "test@test.com",
		"password": "12345678"
	}
}'
```

The Healthnet API uses [Jason Web Tokens (JWT)](https://jwt.io/) for authentication. Make sure you are registered as a user first, then send a request to the `/auth` endpoint to receive a valid token:

### HTTP Request

`POST http://healthnetz.herokuapp.com/v1/auth`

### Arguments

Parameter | Required | Description
--------- | ------- | -----------
email | Yes | Registered user's e-mail address.
password | Yes | Registered user's password

<aside class="warning">
If the credentials are invalid, the endpoint will return 404 Not Found status
</aside>

# Users

## Get All Users

```http
GET /v1/users HTTP/1.1
Host: healthnetz.herokuapp.com
Accept: application/vnd
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "data": [
    {
      "id": "1",
      "type": "users",
      "attributes": {
        "email": "test@test.com",
        "first_name": "John",
        "last_name": "Salchichon",
        "title": "Dr.",
        "location": "Taiwan",
        "institution": "McKay Hospital",
        "date_of_birth": "2017-05-23",
        "phone_number": "094521209"
      },
      "relationships": {
        "work_experiences": {
          "data": [
            {
              "id": "1",
              "type": "work_experiences"
            }
          ]
        },
        "educations": {
          "data": [
            {
              "id": "1",
              "type": "educations"
            }
          ]
        }
      }
    }
  ]
}
```

```shell
curl http://healthnetz.herokuapp.com/v1/users
  -X GET
  -H "Accept: application/vnd"
```

This endpoint retrieves all users.

### HTTP Request

`GET http://healthnetz.herokuapp.com/v1/users`

## Get a Specific User

```http
GET /v1/users/:id HTTP/1.1
Host: healthnetz.herokuapp.com
Accept: application/vnd
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "data": {
    "id": "1",
    "type": "users",
    "attributes": {
      "email": "test@test.com",
      "first_name": "John",
      "last_name": "Salchichon",
      "title": "Dr.",
      "location": "Taiwan",
      "institution": "McKay Hospital",
      "date_of_birth": "2017-05-23",
      "phone_number": "094521209"
    },
    "relationships": {
      "work_experiences": {
        "data": [
          {
            "id": "1",
            "type": "work_experiences"
          }
        ]
      },
      "educations": {
        "data": [
          {
            "id": "1",
            "type": "educations"
          }
        ]
      }
    }
  }
}
```

```shell
curl http://healthnetz.herokuapp.com/v1/users/:id
  -X GET
  -H "Accept: application/vnd"
```

This endpoint retrieves a specific user.

### HTTP Request

`GET http://healthnetz.herokuapp.com/v1/users/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the user to retrieve


## Update a User

```http
PUT /v1/users/:id HTTP/1.1
Host: healthnetz.herokuapp.com
Accept: application/vnd
Content-Type: application/vnd.api+json

{
 "data": {
    "type": "users",
    "attributes": {
  	  "email": "sarah2@test.com"
    }
  }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "data": {
    "id": "1",
    "type": "users",
    "attributes": {
      "email": "sarah2@test.com",
      "first_name": "John",
      "last_name": "Salchichon",
      "title": "Dr.",
      "location": "Taiwan",
      "institution": "McKay Hospital",
      "date_of_birth": "2017-05-23",
      "phone_number": "094521209"
    },
    "relationships": {
      "work_experiences": {
        "data": [
          {
            "id": "1",
            "type": "work_experiences"
          }
        ]
      },
      "educations": {
        "data": [
          {
            "id": "1",
            "type": "educations"
          }
        ]
      }
    }
  }
}
```

```shell
curl http://healthnetz.herokuapp.com/v1/users/:id
  -X PUT
  -H "Accept: application/vnd"
  -H "Content-Type: application/vnd.api+json"
  -d '{
   "data": {
      "type": "users",
      "attributes": {
    	"email": "sarah2@test.com"
      }
    }
  }'
```

Use this endpoint to update an existing user's information. Any parameters not provided will be left unchanged.

### HTTP Request

`PUT/PATCH http://healthnetz.herokuapp.com/v1/users/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the user to retrieve

### Arguments

Parameter | Description
--------- | -----------
email | The e-mail of the user
password | The password of the user
first_name | A detailed description of the doctor's professional experience.
last_name | A detailed description of the doctor's educational background.
title | User's professional title
location | User's current location
institution | Current institution where the user works
date\_of\_birth | Format: `YYYY-MM-DD`
phone_number | User's local phone number

## Delete a User

```http
DELETE /v1/users/:id HTTP/1.1
Host: healthnetz.herokuapp.com
Accept: application/vnd
```

```http
HTTP/1.1 204 No Content
Content-Type: application/json
```

```shell
curl http://healthnetz.herokuapp.com/v1/users/:id
  -X DELETE
  -H "Accept: application/vnd"
```

Permanently deletes a user. This cannot be undone and all user data will be lost.

### HTTP Request

`DELETE http://healthnetz.herokuapp.com/v1/users/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the user

# User Work Experiences

User work experience items are stored and managed separately. The user ID is passed in the URL.

## Add Work Experience

```http
POST /v1/users/:user_id/work_experiences HTTP/1.1
Host: healthnetz.herokuapp.com
Accept: application/vnd
Content-Type: application/vnd.api+json

{
	"data": {
    "type": "work_experiences",
    "attributes": {
      "title": "Software Engineer",
      "company": "Apple",
      "location": "USA",
      "start_year": "2017",
      "current": true,
      "description": "Job description"
		}
	}
}
```
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
	"data": {
	  "id": 5,
		"type": "work_experiences",
	  "attributes": {
	    "title": "Software Engineer",
      "company": "Apple",
      "location": "USA",
      "start_year": "2017",
      "end_year": null,
      "current": true,
      "description": "Job description"
		}
	}
}
```

```shell
curl http://healthnetz.herokuapp.com/v1/users/:user_id/work_experiences
  -X POST
  -H "Accept: application/vnd"
  -H "Content-Type: application/x-www-form-urlencoded"
  -d '{
	"data": {
		"type": "work_experiences",
	  "attributes": {
	    "title": "Software Engineer",
      "company": "Apple",
      "location": "USA",
      "start_year": "2017",
      "current": true,
      "description": "Job description"
		}
	}
}'
```

Adds a new work experience item for a user.

### HTTP Request

`POST http://healthnetz.herokuapp.com/v1/users/:user_id/work_experiences`

### URL Parameters

Parameter | Description
--------- | -----------
user_id | The ID of the user

### Arguments

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
title | String | Yes | Job title
company | String | Yes | Job's company
location | String | Yes | Job's location (country)
start_year | String | Yes | Year when the user started this job
end_year | String | No | Year when the user finished this job, if not current
current | Boolean | Yes | If this job is the user's current job.
description | Text | Yes | Job description

## Update Work Experience

```http
PUT/PATCH /v1/users/:user_id/work_experiences/:id HTTP/1.1
Host: healthnetz.herokuapp.com
Accept: application/vnd
Content-Type: application/vnd.api+json

{
	"data": {
    "type": "work_experiences",
    "attributes": {
      "location": "Japan",
		}
	}
}
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"data": {
	  "id": 5,
		"type": "work_experiences",
	  "attributes": {
	    "title": "Software Engineer",
      "company": "Apple",
      "location": "Japan",
      "start_year": "2017",
      "end_year": null,
      "current": true,
      "description": "Job description"
		}
	}
}
```

```shell
curl http://healthnetz.herokuapp.com/v1/users/:user_id/work_experiences/:id
  -X POST
  -H "Accept: application/vnd"
  -H "Content-Type: application/x-www-form-urlencoded"
  -d '{
	"data": {
		"type": "work_experiences",
	  "attributes": {
      "location": "Japan",
		}
	}
}'
```

Update an existing user's work experience item.

### HTTP Request

`PUT/PATCH http://healthnetz.herokuapp.com/v1/users/:user_id/work_experiences/:id`

### URL Parameters

Parameter | Description
--------- | -----------
user_id | The ID of the user
id | The work experience item's ID

### Arguments

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
title | String | Yes | Job title
company | String | Yes | Job's company
location | String | Yes | Job's location (country)
start_year | String | Yes | Year when the user started this job.
end_year | String | No | Year when the user finished this job, if not current.
current | Boolean | Yes | If this job is the user's current job.
description | Text | Yes | Job description

## Delete a Work Experience

```http
DELETE /v1/users/:user_id/work_experiences/:id HTTP/1.1
Host: healthnetz.herokuapp.com
Accept: application/vnd
```

```http
HTTP/1.1 204 No Content
Content-Type: application/json
```

```shell
curl http://healthnetz.herokuapp.com/v1/users/:user_id/work_experiences/:id
  -X DELETE
  -H "Accept: application/vnd"
```

Permanently deletes a user work experience. This cannot be undone.

### HTTP Request

`DELETE http://healthnetz.herokuapp.com/v1/users/:user_id/work_experiences/:id`

### URL Parameters

Parameter | Description
--------- | -----------
user_id | The ID of the user
id | The work experience item's ID

# User Educations

User education items are stored and managed separately. The user ID is passed in the URL.

## Add Education

```http
POST /v1/users/:user_id/educations HTTP/1.1
Host: healthnetz.herokuapp.com
Accept: application/vnd
Content-Type: application/vnd.api+json

{
	"data": {
    "type": "educations",
    "attributes": {
      "school": "UNITEC",
      "degree": "Ing. Sistemas",
      "field": "Computer Science",
      "description": "Blah blah blah",
      "start_year": "2008",
      "end_year": "2013"
		}
	}
}
```
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
	"data": {
	  "id": 1,
    "type": "educations",
    "attributes": {
      "school": "UNITEC",
      "degree": "Ing. Sistemas",
      "field": "Computer Science",
      "description": "Blah blah blah",
      "start_year": "2008",
      "end_year": "2013",
      "current": false
		}
	}
}
```

```shell
curl http://healthnetz.herokuapp.com/v1/users/:user_id/educations
  -X POST
  -H "Accept: application/vnd"
  -H "Content-Type: application/x-www-form-urlencoded"
  -d '{
	"data": {
		"type": "educations",
    "attributes": {
      "school": "UNITEC",
      "degree": "Ing. Sistemas",
      "field": "Computer Science",
      "description: "Blah blah blah",
      "start_year": "2008",
      "end_year": "2013"
		}
	}
}'
```

Adds a new education item for a user.

### HTTP Request

`POST http://healthnetz.herokuapp.com/v1/users/:user_id/educations`

### URL Parameters

Parameter | Description
--------- | -----------
user_id | The ID of the user

### Arguments

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
school| String | Yes | The education institution
degree | String | Yes | The diploma/degree obtained from the school
field | String | Yes | Specific field of the degree
start_year | String | Yes | Year of initial enrollment in the school
end_year | String | No | Year when studies were finished
current | Boolean | No | If the user still has not received this diploma.
description | Text | Yes | Description about the experience

## Update Education

```http
PUT/PATCH /v1/users/:user_id/educations/:id HTTP/1.1
Host: healthnetz.herokuapp.com
Accept: application/vnd
Content-Type: application/vnd.api+json

{
	"data": {
    "type": "educations",
    "attributes": {
      "school": "Harvard",
		}
	}
}
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"data": {
	  "id": 1,
    "type": "educations",
    "attributes": {
      "school": "Harvard",
      "degree": "Ing. Sistemas",
      "field": "Computer Science",
      "description": "Blah blah blah",
      "from_year": "2008",
      "to_year": "2013",
      "current": false
		}
	}
}
```

```shell
curl http://healthnetz.herokuapp.com/v1/users/:user_id/educations/:id
  -X POST
  -H "Accept: application/vnd"
  -H "Content-Type: application/x-www-form-urlencoded"
  -d '{
	"data": {
		"type": "educations",
	  "attributes": {
      "school": "Harvard",
		}
	}
}'
```

Update an existing user's education item.

### HTTP Request

`PUT/PATCH http://healthnetz.herokuapp.com/v1/users/:user_id/educations/:id`

### URL Parameters

Parameter | Description
--------- | -----------
user_id | The ID of the user
id | The education item's ID

### Arguments

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
school| String | Yes | The education institution
degree | String | Yes | The diploma/degree obtained from the school
field | String | Yes | Specific field of the degree
start_year | String | Yes | Year of initial enrollment in the school
end_year | String | No | Year when studies were finished
current | Boolean | No | If the user still has not received this diploma.
description | Text | Yes | Description about the experience

## Delete User Education

```http
DELETE /v1/users/:user_id/educations/:id HTTP/1.1
Host: healthnetz.herokuapp.com
Accept: application/vnd
```

```http
HTTP/1.1 204 No Content
Content-Type: application/json
```

```shell
curl http://healthnetz.herokuapp.com/v1/users/:user_id/educations/:id
  -X DELETE
  -H "Accept: application/vnd"
```

Permanently deletes a user education item. This cannot be undone.

### HTTP Request

`DELETE http://healthnetz.herokuapp.com/v1/users/:user_id/educations/:id`

### URL Parameters

Parameter | Description
--------- | -----------
user_id | The ID of the user
id | The education item's ID

# User Certificates

User certificate items are stored and managed separately. The user ID is passed in the URL.

## Add Certificate

```http
POST /v1/users/:user_id/certificates HTTP/1.1
Host: healthnetz.herokuapp.com
Accept: application/vnd
Content-Type: application/vnd.api+json

{
	"data": {
    "type": "certificates",
    "attributes": {
      "title": "Limb preservation and salvage",
      "granted_by": "The American Board of Multiple Specialties in Podiatry",
      "year": "2010"
		}
	}
}
```
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
	"data": {
	  "id": 1,
    "type": "certificates",
    "attributes": {
      "title": "Limb preservation and salvage",
      "granted_by": "The American Board of Multiple Specialties in Podiatry",
      "year": "2010"
		}
	}
}
```

```shell
curl http://healthnetz.herokuapp.com/v1/users/:user_id/certificates
  -X POST
  -H "Accept: application/vnd"
  -H "Content-Type: application/x-www-form-urlencoded"
  -d '{
	"data": {
		"type": "certificates",
    "attributes": {
      "title": "Limb preservation and salvage",
      "granted_by": "The American Board of Multiple Specialties in Podiatry",
      "year": "2010"
		}
	}
}'
```

Adds a new certificate item for a user.

### HTTP Request

`POST http://healthnetz.herokuapp.com/v1/users/:user_id/certificates`

### URL Parameters

Parameter | Description
--------- | -----------
user_id | The ID of the user

### Arguments

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
title| String | Yes | The certificate's title
granted_by | String | Yes | Institution that granted the certificate
year | String | Yes | Year when the certificate was received

## Update Certificate

```http
PUT/PATCH /v1/users/:user_id/certificates/:id HTTP/1.1
Host: healthnetz.herokuapp.com
Accept: application/vnd
Content-Type: application/vnd.api+json

{
	"data": {
    "type": "certificates",
    "attributes": {
      "year": "2000"
		}
	}
}
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"data": {
	  "id": 1,
    "type": "certificates",
    "attributes": {
      "title": "Limb preservation and salvage",
      "granted_by": "The American Board of Multiple Specialties in Podiatry",
      "year": "2000"
		}
	}
}
```

```shell
curl http://healthnetz.herokuapp.com/v1/users/:user_id/certificates/:id
  -X POST
  -H "Accept: application/vnd"
  -H "Content-Type: application/x-www-form-urlencoded"
  -d '{
	"data": {
		"type": "certificates",
	  "attributes": {
      "year": "2000"
		}
	}
}'
```

Update an existing user's certificate.

### HTTP Request

`PUT/PATCH http://healthnetz.herokuapp.com/v1/users/:user_id/certificates/:id`

### URL Parameters

Parameter | Description
--------- | -----------
user_id | The ID of the user
id | The certificate ID

### Arguments

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
title| String | Yes | The certificate's title
granted_by | String | Yes | Institution that granted the certificate
year | String | Yes | Year when the certificate was received

## Delete User Certificate

```http
DELETE /v1/users/:user_id/certificates/:id HTTP/1.1
Host: healthnetz.herokuapp.com
Accept: application/vnd
```

```http
HTTP/1.1 204 No Content
Content-Type: application/json
```

```shell
curl http://healthnetz.herokuapp.com/v1/users/:user_id/certificates/:id
  -X DELETE
  -H "Accept: application/vnd"
```

Permanently deletes a user's certificate. This cannot be undone.

### HTTP Request

`DELETE http://healthnetz.herokuapp.com/v1/users/:user_id/certificates/:id`

### URL Parameters

Parameter | Description
--------- | -----------
user_id | The ID of the user
id | The certificate ID