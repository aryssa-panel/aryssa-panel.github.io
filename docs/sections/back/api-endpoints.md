# Endpoints Admin Panel



## 
| Method | HTTP requests        | Description    | Authorization required |
|--------|----------------------|----------------|------------------------|
| `POST` | `api/admin/login`    | Authorization  | No                     |
| `GET`  | `api/admin/user/:id` | Get user by id | Yes                    |





---
### Authorization:

`POST` | `/api/admin/login`<br>

body request:
```json
{
  "username": "toby",
  "password": "password"
}
```

!!! success "Successful response: 👌"

    ```json
    {
    "user": {
        "id": 1,
        "email": "admin@aryssa.com",
        "username": "admin",
        "bio": "",
        "image": "",
        "name": "",
        "roleId": 1,
        "isLocked": false,
        "created_at": "2022-12-20T23:10:36.475Z",
        "updated_at": "2022-12-20T23:10:36.475Z",
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI...."
        }
    }
    ```

!!! bug "Failure response: 🚧"

    ```json
    {
        "statusCode": 401,
        "message": "Unauthorized"
    }
    ```
---
### Get current user

`GET` | `/api/admin/user`<br>

Authorization required (bearer token jwt)

!!! success "Successful response: 👌"

    ```json
    {
    "user": {
        "id": 1,
        "email": "admin@aryssa.com",
        "username": "admin",
        "bio": "",
        "image": "",
        "name": "",
        "roleId": 1,
        "isLocked": false,
        "created_at": "2022-12-20T23:10:36.475Z",
        "updated_at": "2022-12-20T23:10:36.475Z"
        }
    }
    ```
!!! bug "Failure response: 🚧"
    
    if token not valid
    ```json
    {
        "statusCode": 401,
        "message": "Unauthorized"
    }
    ```
---
### Get user by id

`GET` | `/api/admin/user/:id`<br>

Authorization required (bearer token jwt)

!!! success "Successful response: 👌"

    ```json
    {
    "user": {
        "id": 4,
        "email": "toby@gmail.com",
        "username": "toby",
        "bio": "",
        "image": "",
        "name": "",
        "roleId": 3,
        "isLocked": false,
        "created_at": "2022-12-20T23:10:36.475Z",
        "updated_at": "2022-12-20T23:10:36.475Z"
        }
    }
    ```
!!! bug "Failure response: 🚧"

    if token not valid
    ```json
    {
        "statusCode": 401,
        "message": "Unauthorized"
    }
    ```
---
### Get user list

`GET` | `/api/admin/user/list`<br>

Authorization required (bearer token jwt)

!!! success "Successful response: 👌"

    ```json
    {
	"users": [
		{
			"id": 1,
			"email": "admin@aryssa.com",
			"username": "admin",
			"bio": "",
			"image": "",
			"name": "",
			"roleId": 1,
			"isLocked": false,
			"created_at": "2022-12-20T23:10:36.475Z",
			"updated_at": "2022-12-20T23:10:36.475Z"
		},
		{
			"id": 2,
			"email": "admin2@aryssa.com",
			"username": "admin2",
			"bio": "",
			"image": "",
			"name": "",
			"roleId": 1,
			"isLocked": false,
			"created_at": "2022-12-20T23:10:36.477Z",
			"updated_at": "2022-12-20T23:10:36.477Z"
		}
	]
    }
    ```
!!! bug "Failure response: 🚧"

    if token not valid
    ```json
    {
        "statusCode": 401,
        "message": "Unauthorized"
    }
    ```
---
### Update user by id

`PATCH` | `/api/admin/user/:id`<br>

Authorization required (bearer token jwt)

- users with `roleId: 1` can edit **everyone** 
- users with `roleId: 2` or `roleId: 3` can only edit **themselves**

## 
| roleId | description |
|--------|-------------|
| 1      | admin       |
| 2      | editor      |
| 3      | user        |




body request:

all fields are optional
```json
{
  "email": "toby@gmail.com",
  "username": "admin",
  "bio": "some text here",
  "image": "any.png",
  "name": "alex",
  "roleId": 1, /* can change only admin (roleId: 1) */
  "isLocked": false, /* can change only admin (roleId: 1) */
}
```
!!! success "Successful response: 👌"

    ```json
    {
    "user": {
        "id": 4,
        "email": "toby@gmail.com",
        "username": "toby",
        "bio": "some text here",
        "image": "any.png",
        "name": "alex",
        "roleId": 1,
        "isLocked": false,
        "created_at": "2022-12-20T23:10:36.475Z",
        "updated_at": "2022-12-20T23:10:36.475Z"
        }
    }
    ```
!!! bug "Failure response: 🚧"

    if token not valid
    ```json
    {
        "statusCode": 401,
        "message": "Unauthorized"
    }
    ```

!!! bug "Failure response: 🚧"

    if the field from the query body is not unique.
    For example the `username` and `email` fields must be unique in the database

    ```json
    {
        "statusCode": 422,
        "message": "Unprocessable entity"
    }
    ```