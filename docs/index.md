# NightLight Studios API

## Getting Started
### API URL 
To use the API, you need to send a request to the following URL:

`http://litelearn.rickokkersen.myds.me/api/v2/{object}/{action}.php`

For example, to get the data for a user, use the 'user' object like this:

`http://litelearn.rickokkersen.myds.me/api/v2/user/{action}.php`

### Possible objects
This is a list of the existing objects:

- user (get/push information about a user)
- iao (get/push information about Ins and Outs) - Coming Soon

### API authentication 

Because we are dealing with sensitive data about people, you need to verify your API request. You can do this using an API key. In every request, you need to use `{"api_key": "your api key"}`. To get an API key, get in touch with us.

## user
### Check user existance
Send a request to

`http://litelearn.rickokkersen.myds.me/api/v2/user/checkemail.php`

With the following JSON encoded data:
```
{
  "api_key": "apikey",
  "email": "testuser@test.com"
}
```
This can return the following data:

HTTP code | JSON response | Explaination
--- | --- | ---
**503** | `{"message": "empty"}` | if "email" is not specified, or empty string
**400** | `{"message": "noemail"}` | if the value of "email" is not a valid emailaddress
**404** | `{"message": "false"}` | if user does not exist in DB
**409** | `{"message": "multiple"}` | if useremail does exist, but DB returns multiple values
**200** | `{"message": "true"}` | if user exists in DB
**401** | `{"message": "wrongapikey"}` | if API key is not valid

### Check user password

Send a request to

`http://litelearn.rickokkersen.myds.me/api/v2/user/checkpassword.php`

With the following JSON encoded data:
```
{
  "api_key": "apikey",
  "email": "testuser@test.com",
  "password": "test1234"
}
```
This can return the following data:

HTTP code | JSON response | Explaination
--- | --- | ---
**200** | `{"message": "correct", "authToken": "randomtoken"}` | if user exists in DB and password is correct
**500** | `{"message": "unexpectederror"}` | if server DB insert failed!
**400** | `{"message": "wrongpassword"}` | if user exists in DB but password is incorrect
**401** | `{"message": "wrongapikey"}` | if API key is invalid

### Check user token (check login status)

Send a request to:

`http://litelearn.rickokkersen.myds.me/api/v2/user/checktoken.php`

With the following JSON encoded data:

```
{
  "api_key": "apikey",
  "authToken": "usertoken"
}
```
This can return the following data:

HTTP code | JSON response | Explaination
--- | --- | ---
**400** | `{"message": "notoken"}` | if token is not set, or set to null
**200** | `{"message": "valid"}` | if token is valid
**403** | `{"message": "invalid"}` | if token is not valid
**401** | `{"message": "wrongapikey"}` | if API key is invalid

### User sign up

Send a request to:

`http://litelearn.rickokkersen.myds.me/api/v2/user/signup.php`

With the following JSON encoded data:

```
{
  "api_key": "apikey",
  "first_name": "firstname",
  "last_name": "lastname",
  "email": "emailaddress",
  "password": "plaintextpassword"
}
```
This can return the following data:

HTTP code | JSON response | Explaination
--- | --- | ---
**201** | `{"message": "created"}` | User successfully created
**503** | `{"message": "error"}` | DB error, user not created
**400** | `{"message": "dataincomplete"}` | Not all fields are filled in
**401** | `{"message": "wrongapikey"}` | If API key is invalid

## iao
Coming soon!!

### Get all posts
Send a request to:

`http://litelearn.rickokkersen.myds.me/api/v2/iao/getall.php`

With the following JSON encoded data:

```
{
  "api_key": "apikey"
}
```
This can return the following data:

HTTP code | JSON response | Explaination
--- | --- | ---
**200** | `{...array of posts...}` | JSON array containing all post data
**404** | `{"message": "notfound"}` | No posts were found
**401** | `{"message": "wrongapikey"}` | If API key is invalid

### Get one post

### Create post

### Delete post

### Report post
