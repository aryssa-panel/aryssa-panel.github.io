# Endpoints
### Authentication Header:
You can read the authentication header from the headers of the request

Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5c....
## Users
### Authentication:
`POST /api/admin/login`
```json
{
    "username": "admin",
    "password": "admin"
}
```
Required fields: `email`, `password` <br>
No authentication required, returns User:
```json
{
  "user": {
    "email": "admin@aryssa.com",
    "username": "admin",
    "bio": "",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImFkbWluIiwic3ViIjoxLCJpYXQiOjE2NzAyNzc3NDQsImV4cCI6MTY3MDI5NTc0NH0.V2C9jvMHYg2osgYUHOhFskdA0I7lu-lsw1Jxh03mjGM"
  }
}
```
### Get Current Admin User
`GET api/admin/user` <br>
Authentication required, returns a User that's the current user
```json
{
    "user": {
        "id": 1,
        "email": "admin@aryssa.com",
        "username": "admin",
        "bio": "",
        "image": ""
    }
}
```
### List Users
`GET /api/admin/user/list`<br>
Authentication required, returns array of users 
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
            "created_at": "2022-12-05T20:29:12.766Z",
            "updated_at": "2022-12-05T20:29:12.766Z"
        }
    ]
}
```
## Tags