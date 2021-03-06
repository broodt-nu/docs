# Authentication / Authorization

{% api-method method="post" host="https://api.broodt.nu" path="/auth/register" %}
{% api-method-summary %}
Register Account
{% endapi-method-summary %}

{% api-method-description %}
Create a user account.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="password" type="string" required=true %}
min:8 - User Password
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=true %}
max:255\|unique - User Email
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=true %}
max:50\|alpha\_num - User Name
{% endapi-method-parameter %}

{% api-method-parameter name="captcha\_response" type="string" required=true %}
The response of Google reCaptcha V2 Checkbox
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Account successfully created.
{% endapi-method-response-example-description %}

```javascript
{
  "name": "fooBar",
  "email": "fooBar@example.com",
  "updated_at": "2019-04-26 18:15:31",
  "created_at": "2019-04-26 18:15:31",
  "id": 1
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
No or invalid captcha\_respond provided
{% endapi-method-response-example-description %}

```javascript
{
  "error": "invalid captcha"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}
Incorrect or empty fields passed
{% endapi-method-response-example-description %}

```javascript
{
  "captcha_response": [
    "The captcha response field is required."
  ],
  "name": [
    "The name field is required."
  ],
  "email": [
    "The email field is required."
  ],
  "password": [
    "The password field is required."
  ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://api.broodt.nu" path="/auth/verify" %}
{% api-method-summary %}
Verify Email
{% endapi-method-summary %}

{% api-method-description %}
Activate your account
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="verify\_email\_token" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Account verification successful
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}
Incorrect or empty fields passed
{% endapi-method-response-example-description %}

```javascript
{
  "verify_email_token": [
    "The selected verify email token is invalid."
  ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://api.broodt.nu" path="/auth/login" %}
{% api-method-summary %}
Login
{% endapi-method-summary %}

{% api-method-description %}
Generate an "session\_uuid", "access\_token" and "refresh\_token"
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="email" type="string" required=true %}
max:255\|unique - User Email
{% endapi-method-parameter %}

{% api-method-parameter name="password" type="string" required=true %}
min:8 - User Password
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Login successful
{% endapi-method-response-example-description %}

```javascript
{
  "session_uuid": "88621fa0-8d56-11e9-8b9a-4dacaf90652b",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9sb2NhbGhvc3Q6ODA4MCIsImF1ZCI6Imh0dHBzOlwvXC9icm9vZHQubnUiLCJzdWIiOjIsInN1Yl9pcCI6Ils6OjFdIiwiaWF0IjoxNTU2Mjk5MjIxLCJleHAiOjE1NTYzMDAxMjF9.YG8YcS4TxqOwOSPTaOtkFkKoaH4hjaFTwdE63cWexCKaKMdx9ewmTPCFcfDa4uSTJG9RixskFEwU0MjvBppyCg",
  "refresh_token": "wLVJkrwcT3YQHAjs2KKyY3f81PTssZuT"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Invalid credentials
{% endapi-method-response-example-description %}

```javascript
{
  "errors": {
    "email or password": [
      "is invalid"
    ]
  }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}
Incorrect or empty fields passed
{% endapi-method-response-example-description %}

```javascript
{
  "email": [
    "The email field is required."
  ],
  "password": [
    "The password field is required."
  ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://api.broodt.nu" path="/auth/logout" %}
{% api-method-summary %}
Logout
{% endapi-method-summary %}

{% api-method-description %}
Revoke the "refresh\_token"
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
'Bearer ' + access\_token
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Refresh successful
{% endapi-method-response-example-description %}

```javascript

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://api.broodt.nu" path="/auth/refresh" %}
{% api-method-summary %}
Refresh
{% endapi-method-summary %}

{% api-method-description %}
Refresh the users "access\_token" using the "session\_uuid" and "refresh\_token"
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="refresh\_token" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="session\_uuid" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9sb2NhbGhvc3Q6ODA4MCIsInN1YiI6MSwic3ViX2lwIjoiWzo6MV0iLCJzZXNzaW9uIjoiODg2MjFmYTAtOGQ1Ni0xMWU5LThiOWEtNGRhY2FmOTA2NTJiIiwiaWF0IjoxNTYwMzczODY1LCJleHAiOjE1NjAzNzQ3NjV9.w_NDGZsKrpijWU6CuKvYa7-CScG_iSDyjpCL1K0Ttr03pxzdh-vIZuPwJF3VjEPiwWL_-9ZYP_pIw3k5pfDnoOy9wNwVho5cQWpU7d6P0E-xVqdHkOcu_ofGc80XGI6-S4C0Pv5sDQrmJY4LxknSBNtT32ywhrJ10RNT5nkRqb1DhzI9KKBCr1oJSyldRm6Dtl61CVzbUWrspiN1EHknFYXftNpvgqek_8cgbZKvsarZCDLpqpybWZy0eYgVYnVGTI6OdgRIsegB4mZAhVYbZ64-pvAWCP3VHFN13CAeP-ydHs49dI4glDa65IO2RnimxXpHNqL4Y-c2fbn2s0GiEw",
  "session_uuid": "88621fa0-8d56-11e9-8b9a-4dacaf90652b",
  "refresh_token": "AvXJ5jK9aizmWtdTpNFexzUOeduoGVjDZlgwjWsA8M6gMmts26I1RlXkI984Kd1Wm8Bz2JCQLZUHFfURUeUjDV85qovSQPGttPrCzTwknkEtMKCC1lSYtlOrQnnBUzX0ukz73OEgjAwEHOiEsoQ6LLGJUts8hkzve44MsQBRmAL21uN8LjC7yyTbanTYrTMTi3kevfhoVMkjKxaRHAJhFruyvm3Dv3zFW0OXx5aGTBiGEMvbJtd99lczpnDaEgl2"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Invalid "session\_uuid" and "refresh\_token" combination
{% endapi-method-response-example-description %}

```javascript
false
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}
Incorrect or empty fields passed
{% endapi-method-response-example-description %}

```javascript
{
  "session_uuid": [
    "validation.required"
  ],
  "refresh_token": [
    "validation.required"
  ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://api.broodt.nu" path="/auth/reset/request" %}
{% api-method-summary %}
Request Reset Password
{% endapi-method-summary %}

{% api-method-description %}
Request a password reset link
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="captcha\_response" type="string" required=true %}
The response of Google reCaptcha V2 Checkbox
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=true %}
max:255\|unique - Email
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Reset request sent
{% endapi-method-response-example-description %}

```javascript

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}
Incorrect or empty fields passed
{% endapi-method-response-example-description %}

```javascript
{
  "email": [
    "The selected email is invalid."
  ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://api.broodt.nu" path="/auth/reset" %}
{% api-method-summary %}
Reset Password
{% endapi-method-summary %}

{% api-method-description %}
Reset the users password
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="password" type="string" required=true %}
min:8 - Password
{% endapi-method-parameter %}

{% api-method-parameter name="reset\_password\_token" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Password reset successful
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "reset_password_token": [
    "The selected reset password token is invalid."
  ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

