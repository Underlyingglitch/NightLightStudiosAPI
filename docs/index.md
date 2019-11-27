# StellaMarisAPI

## Check user existance 

Send a request to

`http://stellamaris.rickokkersen.myds.me/api/v2/user/check.php`

With the following JSON encoded data:
```
{
  "email": "testuser@test.com"
}
```
This can return the following data:

Input | HTTP code | JSON response | Explaination
--- | --- | --- | ---
*Still* | `renders` | **nicely**
`{"email": ""}` (or nothing at all) | **503** | `{"message": "empty"}` | if "email" is not specified, or empty string
`{"email": "this is some text"}` | **400** | `{"message": "noemail"}` | if the value of "email" is not a valid emailaddress
`{"email": "notexist@test.com"}` | **404** | `{"message": "false"}` | if user does not exist in DB
`{"email": "testuser@test.com"}` | **409** | `{"message": "multiple"}` | if useremail does exist, but DB returns multiple values
`{"email": "testuser@test.com"}` | **200** | `{"message": "true"}` | if user exists in DB

## Check user password

Send a request to

`http://stellamaris.rickokkersen.myds.me/api/v2/user/checkpassword.php`

With the following JSON encoded data:
```
{
  "email": "testuser@test.com",
  "password": "test1234"
}
```
This can return the following data:

Input | HTTP code | JSON response | Explaination
--- | --- | --- | ---
*Still* | `renders` | **nicely**
`{"email": "", "password": ""}` (or nothing at all) | **503** | `{"message": "empty"}` | if "email" is not specified, or empty string
`{"email": "this is some text", "password": "some password"}` | **400** | `{"message": "noemail"}` | if the value of "email" is not a valid emailaddress
`{"email": "notexist@test.com", "password": "test1234"}` | **404** | `{"message": "false"}` | if user does not exist in DB
`{"email": "testuser@test.com", "password": "test1234"}` | **409** | `{"message": "multiple"}` | if user does exist, but DB returns multiple values (DB eror)
`{"email": "testuser@test.com", "password": "test1234"}` | **200** | `{"message": "correct"}` | if user exists in DB and password is correct
`{"email": "testuser@test.com", "password": "incorrect"}` | **401** | `{"message": "worngpassword"}` | if user exists in DB but password is incorrect
