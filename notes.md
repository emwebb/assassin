# R U Assassins

## Website API

`token`'s are used for stateless login information. The browser should store the token. The format for a token when sent to the server should be the token, followed by the unix time stamp as an integer to the 65536 milliseconds. (Unix Time Stamp in ms right shifted by 16), all md5 hashed.

i.e. 
```javascript=
md5("mytoken" + ((new Date()).getTime() >>> 16))
```

### Register

#### POST
```
{
    "username": string,
    "displayName": string,
    "password": string
}
```

#### RESPONSE
On Success
```
201 CREATED
```
Duplicate Username, or Invalid Password, Or Malformed Request
```
400 BAD REQUEST
```

### Login

#### POST
```
{
    "username": string,
    "password": string
}
```

#### RESPONSE
On Success
```
201 OK
{
    "username": string,
    "token": string,
}
```
On Invalid Username or Password, or Malformed Request
```
400 BAD REQUEST
```

### WhoAmI

#### POST
```
{
    "loginUsername": string,
    "loginToken": string
}
```

#### REPSONSE
```
200 OK
{
    "username": string,
    "displayName": string,
    "isAdmin": boolean
}
```
On Malformed Request
```
400 BAD REQUEST
```
On Not Authorised
```
403 FORBIDDEN
```

### CreateGame

#### POST

```
{
    "loginUsername": string,
    "loginToken": string,
    "gameName": string
}
```

#### RESPONSE

On Success
```
201 CREATED
{
    "gameId": string
}
```

On Malformed Request
```
400 BAD REQUEST
```

On Not Authorised
```
403 FORBIDDEN
```

### StartGame

#### POST

```
{
    "loginUsername": string,
    "loginToken": string,
    "gameId": string
}
```

#### RESPONSE

On Success
```
200 CREATED
```

On Malformed Request
```
400 BAD REQUEST
```

On Not Authorised
```
403 FORBIDDEN
```

### GetMyAdminGames

#### POST
```
{
    "loginUsername": string,
    "loginToken": string
}
```

#### RESPONSE
On Success
```
200 OK
[
    {
        "gameId": string,
        "gameName": string
        "started": boolean
    },...
]
```
On Malformed Request
```
400 BAD REQUEST
```
On Invalid Login
```
403 Forbidden
```

### GetMyMemberGames

#### POST
```
{
    "loginUsername": string,
    "loginToken": string,
}
```

#### RESPONSE
On Success
```
200 OK
[
    {
        "gameId": string,
        "gameName": string,
        "started": boolean
    },...
]
```
On Malformed Request
```
400 BAD REQUEST
```
On Invalid Login
```
403 Forbidden
```

### GetMyTargets
#### POST
```
{
    "loginUsername": string,
    "loginToken": string
}
```
#### RESPONSE
On Success
```
200 OK
[
    {
        "gameId": string,
        "gameName": string,
        "displayName": string,
        "username": string
    },...
]
```
On Malformed Request
```
400 BAD REQUEST
```
On Invalid Login
```
403 Forbidden
```

### GetGameAdmin

#### POST
```
{
    "loginUsername": string,
    "loginToken": string,
    "gameId": string
}
```

#### RESPONSE
On Success
```
200 OK
{
    "displayName": string,
    "username": string
}
```
On Malformed Request
```
400 BAD REQUEST
```
On Invalid Login
```
403 Forbidden
```

### GetGameMembers
```
{
    "loginUsername": string,
    "loginToken": string,
    "gameId": string
}
```

#### RESPONSE
On Success
```
200 OK
[
    {
        "displayName": string,
        "username": string
    },...
]
```
On Malformed Request
```
400 BAD REQUEST
```
On Invalid Login
```
403 Forbidden
```

### Search

#### POST

```
{
    "loginUsername": string,
    "loginToken": string,
    "query": string 
}
```

#### RESPONSE
On Success
```
200 OK
[
    {
        "displayName": string,
        "username": string
    },...
]
```
On Malformed Request
```
400 BAD REQUEST
```

### Invite

#### POST
```
{
    "loginUsername": string,
    "loginToken": string,
    "gameId": string
}
```

#### RESPONSE
On Success
```
200 OK
```
On Malformed Request
```
400 BAD REQUEST
```
On Not Authorised
```
403 FORBIDDEN
```

### GetMyInvites

#### POST
```
{
    "loginUsername": string,
    "loginToken": string
}
```
#### RESPONSE
On Success
```
200 OK
[
    {
        "gameId": string,
        "gameName": string
    },...
]
```
On Malformed Request
```
400 BAD REQUEST
```
On Not Authorised
```
403 FORBIDDEN
```
### AcceptInvite

#### POST
```
{
    "loginUsername": string,
    "loginToken": string,
    "gameId": string 
}
```
#### RESPONSE
On Success
```
200 OK
```
On Malformed Request
```
400 BAD REQUEST
```
On Not Authorised
```
403 FORBIDDEN
```

### RejectInvite

#### POST
```
{
    "loginUsername": string,
    "loginToken": string,
    "gameId": string 
}
```
#### RESPONSE
On Success
```
200 OK
```
On Malformed Request
```
400 BAD REQUEST
```
On Not Authorised
```
403 FORBIDDEN
```


### AssassinationRequest

#### POST
```
{
    "loginUsername": string,
    "loginPassword": string,
    "gameID": string,
    "targetUsername": string
}
```
#### RESPONSE
On Success
```
201 CREATED
```
On Malformed Request
```
400 BAD REQUEST
```
On Not Authorised
```
403 FORBIDDEN
```


### GetAssassinationRequests

#### POST
```
{
    "loginUsername": string,
    "loginPassword": string
}
```

#### RESPONSE
On Success
```
200 OK
[
    {
        "gameId": string,
        "gameName": string,
        "killerDisplayName": string,
        "killerUsername": string
    },...
]
```
On Malformed Request
```
400 BAD REQUEST
```
On Not Authorised
```
403 FORBIDDEN
```

### ApproveAssasination

#### POST
```
{
    "loginUsername": string,
    "loginToken": string,
    "gameId": string,
    "username": string
}
```

#### RESPONSE
On Success
```
200 OK
```
On Malformed Request
```
400 BAD REQUEST
```
On Not Authorised
```
403 FORBIDDEN
```

### RejectAssasination

#### POST
```
{
    "loginUsername": string,
    "loginToken": string,
    "gameId": string,
    "username": string
}
```

#### RESPONSE
On Success
```
200 OK
```
On Malformed Request
```
400 BAD REQUEST
```
On Not Authorised
```
403 FORBIDDEN
```

### GetMyAdminConflicts

#### POST
```
{
    "loginUsername": string,
    "loginPassword": string
}
```

#### RESPONSE
On Success
```
200 OK
[
    {
        "gameId": string,
        "gameName": string,
        "killerUsername": string,
        "killerDisplayName": string,
        "targetUsername": string,
        "targetDisplayName": string
    },...
]
```
On Malformed Request
```
400 BAD REQUEST
```
On Not Authorised
```
403 FORBIDDEN
```

### ForceApproveAssassinate

#### POST
```
{
    "loginUsername": string,
    "loginPassword": string,
    "gameId": string,
    "killerUsername": string,
    "targetUsername": string,
}
```

#### RESPONSE
On Success
```
200 OK
```
On Malformed Request
```
400 BAD REQUEST
```
On Not Authorised
```
403 FORBIDDEN
```

### ForceDenyAssassinate
```
{
    "loginUsername": string,
    "loginPassword": string,
    "gameId": string,
    "killerUsername": string,
    "targetUsername": string,
}
```

#### RESPONSE
On Success
```
200 OK
```
On Malformed Request
```
400 BAD REQUEST
```
On Not Authorised
```
403 FORBIDDEN
```
