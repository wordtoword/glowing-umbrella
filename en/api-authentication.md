---
title: Authentication
category: API
---

Authentication endpoints contain information about user authentication, including access tokens, login, logout, and password reminders.

## Endpoints

### Login

#### login_challenge

Method: `POST` 

Authenticates user with login details.

##### Basic settings

| Parameter | Required/optional | Description | Type |
| :--- | :--- | :--- | :--- |
| login_method | | | |

##### Sample request

```
{
  "email": "test1@aaa.com",
  "password": "12345aaa",
  "login_save": 0
}
```

##### Sample response

```
{
  "grant_token": "a4bc641931c06327c17875f5f92dc41b1f178f1306acfb20daba078c84b32263",
  "status": 0,
  "member_id": 12,
  "info": {
    "validUntil": 1668768282
  },
  "messages": [],
  "errors": []
}
```


#### token

Method: `POST`

Authenticates user with access token.

##### Basic settings

| Parameter | Required/optional | Description | Type |
| :--- | :--- | :--- | :--- |
| use_refresh_token | | Enable the use of refresh token. | Checkbox |
| access_token_lifespan | | Duration of access token validity in seconds. | Integer |
| refresh_token_lifespan | | Duration of refresh token validity (if applicable) in seconds. | Integer |

##### Sample request

```
{

}
```

##### Sample response

```
{

}
```


#### file_access_token

Method: `GET`

Retrieves token for access to files stored in KurocoFiles.

##### Basic settings

| Parameter | Required/optional | Description | Type |
| :--- | :--- | :--- | :--- |
| access_token_lifespan | | Duration of access token validity in seconds. | Integer |

##### Sample request

```
{

}
```

##### Sample response

```
{
  "file_access_token": {
    "value": "86fa070dad5b1b979c8b7080ebbe421e852bb52bc9361d1097af0fae7d3939b0",
    "expiresAt": 1668762577
  }
}
```

#### alias_login

Method: `POST`

Enables user login under an alias or proxy member ID.    

##### Sample request

```
{
  "aliaslogin_id": 2
}
```
[[info]] The member ID you use here must be set up as an allowed proxy for the current user under "[Proxy login permission](https://diverta.gyazo.com/5f9eb8ce1cd5e3e9b39ddd83b0882c6f)" on the member ID information screen. For more details, see [User guide: Member editor](/docs/management/member/#member-editor).

##### Sample response

```
{
  "grant_token": "16ba9c151ac794a9173bf1df9c60da3e230d730eed6bb5c97fa0e2970ac11979",
  "status": 0,
  "member_id": 2,
  "info": {
    "validUntil": 1668770179
  },
  "messages": [],
  "errors": []
}
```

#### logout

Method: `POST`

Logs user out of the authentication session.

##### Sample request

```
{

}
```

##### Sample response

```
{
  "status": 0,
  "messages": [
    "Logged out."
  ],
  "errors": []
}
```

#### reminder

Method: `POST`

Sends a password reminder message to the e-mail address associated with the user account.

##### Sample request

```
{
  "email": "test1@aaa.com"
}
```

##### Sample response

```
{
  "errors": [],
  "messages": [
    "We've sent you an e-mail with the URL to change your password."
  ]
}
```

#### reset_password

Method: `POST`

Resets the user password.

##### Sample request

```
{
  "login_id": "12",
  "current_password": "12345aaa",
  "new_password": "67890aaa"
}
```

##### Sample response

```
{

}
```
