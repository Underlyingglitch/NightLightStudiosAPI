# StellaMarisAPI

## Getting Started
### API URL 
To use the API, you need to send a request to the following URL:

`http://stellamaris.rickokkersen.myds.me/api/v2/{object}/{action}.php`

For example, to get the data for a user, use the 'user' object like this:

`http://stellamaris.rickokkersen.myds.me/api/v2/user/{action}.php`

### Possible objects
This is a list of the existing objects:
- user (get/push information about a user)

### API authentication 

Because we are dealing with sensitive data about people, you need to verify your API request. You can do this using an API key. In every request, you need to use `{"api_key": "your api key"}`. To get an API key, get in touch with us.

## user
### Check user existance
Send a request to

`http://stellamaris.rickokkersen.myds.me/api/v2/user/check.php`

With the following JSON encoded data:
```
{
  "api_key": "apikey",
  "email": "testuser@test.com"
}
```
This can return the following data:

Input | HTTP code | JSON response | Explaination
--- | --- | --- | ---
`{"api_key": "correctkey", "email": ""}` (or nothing at all) | **503** | `{"message": "empty"}` | if "email" is not specified, or empty string
`{"api_key": "correctkey", "email": "this is some text"}` | **400** | `{"message": "noemail"}` | if the value of "email" is not a valid emailaddress
`{"api_key": "correctkey", "email": "notexist@test.com"}` | **404** | `{"message": "false"}` | if user does not exist in DB
`{"api_key": "correctkey", "email": "testuser@test.com"}` | **409** | `{"message": "multiple"}` | if useremail does exist, but DB returns multiple values
`{"api_key": "correctkey", "email": "testuser@test.com"}` | **200** | `{"message": "true"}` | if user exists in DB
`{"api_key": "wrongkey", "email": "testuser@test.com"}` | **401** | `{"message": "wrongapikey"}` | if API key is not valid

### Check user password

Send a request to

`http://stellamaris.rickokkersen.myds.me/api/v2/user/checkpassword.php`

With the following JSON encoded data:
```
{
  "api_key": "apikey",
  "email": "testuser@test.com",
  "password": "test1234"
}
```
This can return the following data:

Input | HTTP code | JSON response | Explaination
--- | --- | --- | ---
`{"api_key": "correctkey", "email": "testuser@test.com", "password": "test1234"}` | **200** | `{"message": "correct", "authToken": "randomtoken"}` | if user exists in DB and password is correct
`{"api_key": "correctkey", "email": "testuser@test.com", "password": "test1234"}` | **500** | `{"message": "unexpectederror"}` | if server DB insert failed!
`{"api_key": "correctkey", "email": "testuser@test.com", "password": "incorrect"}` | **400** | `{"message": "wrongpassword"}` | if user exists in DB but password is incorrect
`{"api_key": "wrongkey", "email": "testuser@test.com", "password": "test1234"}` | **401** | `{"message": "wrongapikey"}` | if API key is invalid
