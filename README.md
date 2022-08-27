# **CubeCraft API** <!-- omit in toc -->
REST(?) API accessible @ https://api.cubecraft.net/

> Quick note!
> This is not a complete documentation. All resources have been documented by researching, discovering, bruteforcing, and trying stuff.
> As of the day I'm writing this, the CubeCraft API is not currently public, and the skins API is protected via Cloudflare's anti-bot protection.
> Plus, these docs are still a work in progress!

## Table of contents <!-- omit in toc -->
- [Root](#root)
  - [Request](#request)
  - [Response](#response)
  - [Status code](#status-code)
  
- [Skins](#skins)
  - [Request](#request-1)
  - [Response](#response-1)
  - [Status code](#status-code-1)
  - [Parameters](#parameters)
    - [`login`](#login)
    - [`format`](#format)
    - [`ratio`](#ratio)
    - [`headOnly`](#headonly)
    - [`displayHairs`](#displayhairs)
    - [`a`](#a)
    - [`w`](#w)
    
- [Stats](#stats)
  - [Request](#request-2)
  - [Response](#response-2)
  - [Parameters](#parameters-1)
    - [`sid`](#sid)
    - [`transport`](#transport)
    - [`EIO`](#eio)
    - [`t`](#t)
      
- [SID](#sid-1)
  - [Request](#request-3)
  - [Response](#response-4)
  - [Parameters](#parameters-2)
    - [`transport`](#transport-1)
    - [`EIO`](#eio-1)
    - [`t`](#t-1)
    
- [MemberSearch](#MemberSearch)
  - [Request](#request-4)
  - [Response](#response-5)
  - [Parameters](#parameters-3)
    - [`q`](#q)
    - [`_xfRequestUri`](#_xfRequestUri)
    - [`_xfWithData`](#t_xfWithData)
    - [`_xfToken`](#_xfToken)
    - [`_xfResponseType`](#_xfResponseType)

- [Ranks](#Ranks)
  - [Request](#request-5)
  - [Response](#response-6)
  - [Parameters](#parameters-4)
    - [`uuid`](#uuid)
---
## Root
### Request
```
GET https://api.cubecraft.net/
```

### Response
```
{"error":"Not authorized."}
```

### Status code
403

---
## Skins
### Request
```
GET https://api.cubecraft.net/skins/
```

### Response
3D render of a Steve skin

### Status code
200

### Parameters
If a parameter is invalid, the server will use the default one, instead of returning an error.
#### `login`
- User UUID, **must** be dashed.
- Type: `string`
- Default: ? (outputs a Steve skin)
#### `format`
- Choose the rendered image's format. As of now, it **always** defaults to PNG.
- Type: `string`
- Default: `PNG`
#### `ratio`
- Modify the size of the image, while keeping the same aspect ratio.
- Type: `float` (positives)
- Default: `1`
#### `headOnly`
- Render only the user's head.
- Type: `bool`
- Default: `false`
#### `displayHairs`
- Render the user's head overlay.
- Type: `bool`
- Default: `true`
#### `a`
- Rotate the model on the x axis.
- Type: `float` (positives and negatives, values are interpreted as degrees)
- Default: `-25`
#### `w`
- Rotate the model on the y axis.
- Type: `float` (positives and negatives, values are interpreted as degrees)
- Default: `35`

parameters to examine:
&wt=-45&abg=0&abd=-30&ajg=-25&ajd=30

---

## Stats

### Request
```
GET https://stats.cubecraft.net/socket.io/
```

### Response
Stats of the currently online players on the CubeCraft Network

### Response
- Type: `application/json`
- Status Code: `200`

**Content:**
- `unique_sessions`: amount of unique sessions made to the network (not working, returning 0)
  - `today`: today
  - `total`: total
- `online_count`: amount of people currently online the Network
  - `total`: counting players on all platforms all together
  - `bedrock`: players on the bedrock server
  - `java_19`: players on the 1.12+ version of the Java server
  - `java_18`: players on the 1.8 version of the Java server (returning 0 since 1.8 is no longer supported on CubeCraft)

### Parameters
A list if all know parameters for this request, if a parameter is invalid, the server will use the default one, instead of returning an error.
#### `sid`
- Session ID, can be obtained at [SID](#sid)
- Type: `string`
- Default: `?`
- Required: `False`
- Allowed options: `session.io valid sid`

#### `transport`
- Info: `socket.io transport protocol`
- Type: `string`
- Default: `None`
- Required: `True`
- Allowed options: `["polling"]`

#### `EIO`
- Info: `the current version of the engine.io protocol`
- Type: `integer`
- Default: `? 3`
- Required: `False`
- Allowed options: `[1, 2, 3, 4]`

#### `t`
- Info: `a hashed timestamp for cache-busting`
- Type: `string`
- Default: `?`
- Required: `False`
- Allowed options: `yeast valid timestamp id`

---
## SID
socket.io session ID required to make arequest to the Stats API

### Request
```
GET https://stats.cubecraft.net/socket.io/
```

### Response
- Type: `application/json`
- Status Code: `200`

**Content:**
- `sid`: the unique session id
- `upgrades`: the list of possible transport upgrades
- `pingInterval`: the 1st parameter for the heartbeat mechanism
- `pingTimeout`: the 2nd parameter for the heartbeat mechanism

### Parameters
A list if all know parameters for this request, if a parameter is invalid, the server will use the default one, instead of returning an error.
#### `transport`
- Info: `socket.io transport protocol`
- Type: `string`
- Default: `None`
- Required: `True`
- Allowed options: `["polling"]`

#### `EIO`
- Info: `the current version of the engine.io protocol`
- Type: `integer`
- Default: `? 3`
- Required: `False`
- Allowed options: `[1, 2, 3, 4]`

#### `t`
- Info: `a hashed timestamp for cache-busting`
- Type: `string`
- Default: `?`
- Required: `False`
- Allowed options: `yeast valid timestamp id`

---
## MemberSearch
Returns list of forums members based on your query

### Request
```
GET https://www.cubecraft.net/index.php?members/find
```

### Response
- Type: `application/json`
- Status Code: `200`

### Parameters
A list if all know parameters for this request, if a parameter is invalid, the server will use the default one, instead of returning an error.
#### `q`
- Info: `search query`
- Type: `string`
- Default: `None`
- Required: `True`
- Allowed options: `any string`

#### `_xfRequestUri`
- Info: `request uri`
- Type: `string`
- Default: `None`
- Required: `False`
- Allowed options: `%2Fmembers%2F`

#### `_xfWithData`
- Info: `??`
- Type: `integer`
- Default: `1`
- Required: `False`
- Allowed options: `1`

#### `_xfToken`
- Info: `authentication token`
- Type: `string`
- Default: `None`
- Required: `True`
- Allowed options: `valid auth token`

#### `_xfResponseType`
- Info: `response type`
- Type: `string`
- Default: `None`
- Required: `False`
- Allowed options: `["json"]`

---
## Ranks
Returns a rank of the provided player

### Request
```
GET https://store-assets.cubecraft.net/v2/store_config.php?
```

### Response
- Type: `application/json`
- Status Code: `200`

### Parameters
A list if all know parameters for this request, if a parameter is invalid, the server will use the default one, instead of returning an error.

#### `uuid`
- Info: `uuid of a player`
- Type: `string`
- Default: `None`
- Required: `True`
- Allowed options: `any string`


_Docs written by The_TecnoKing#7293 & KristN#1234_ & ᲼᲼#3205
