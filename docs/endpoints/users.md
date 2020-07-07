# User Application Endpoints

## Social Auth Login/Register

After getting the social token from either facebook or google using OAuth2, exchange the social token for an access_token that is usable in our application. This endpoint is used for both first-time and returning users, as both scenarios follow the same pipeline.

**Permissions**: Any

**Endpoint**: <http://localhost:8000/auth/convert-token>



        POST DATA = {
          "grant_type": "convert_token",
          "client_id": "<CLIENT_ID>",
          "client_secret": "<CLIENT_SECRET>",
          "backend": "<FACEBOOK/GOOGLE-OAUTH2>",
          "token": "<TOKEN>"
        }

        RESPONSE DATA = {
          "access_token": "<ACCESS_TOKEN>",
          "expires_in": 36000,
          "token_type": "Bearer",
          "scope": "read write",
          "refresh_token": "<REFRESH_TOKEN>"
        }


## Login (Non-Social Auth users)

Login page for returning users. Provide access_token if login_cridentials are valid

**Permissions**: Any

**Endpoint**: <http://localhost:8000/auth/token/>


        POST DATA = {
          "grant_type": "password",
          "client_id": "<CLIENT_ID">,
          "client_secret": "<CLIENT_SECRET>",
          "username": "<USERNAME>",
          "password": "<PASSWORD>"
        }

        RESPONSE DATA = {
          "access_token": "<ACCESS_TOKEN>",
          "expires_in": 36000,
          "token_type": "Bearer",
          "scope": "read write",
          "refresh_token": "<REFRESH_TOKEN>"
        }
## Create User

Create a user with minimum information. Is_configured defaults to false, other information must be provided later (using the update or partial-update endpoints)

**Permissions**: Any

**Endpoint**: <http://localhost:8000/api/users/>

        POST DATA = {
          "first_name": "<FIRST_NAME>",
          "last_name": "<LAST_NAME>",
          "email": "<EMAIL>",
          "password": "<PASSWORD>"
        }

**Validation**:

- [Email Validator](https://docs.djangoproject.com/en/3.0/ref/validators/#emailvalidator)
- [Password Validator](https://docs.djangoproject.com/en/2.0/_modules/django/contrib/auth/password_validation/)

## Retrieve User

Returns entire user profile, only if you are the user owner

**Permissions**: User Owner

**Endpoint**: <http://localhost:8000/api/users/PK/>

        GET REQUEST:
          Authorization: "Bearer <ACCESS_TOKEN>"

## Retrieve Logged in "Me" User

Returns the entire user profile of the account associated with the application access token provided.

**Permissions**: Is Authenticated

**Endpoint**: <http://localhost:8000/api/users/me/>

        GET REQUEST:
          Authorization: "Bearer <ACCESS_TOKEN>"
        RESPONSE DATA = {
          "pk": <PK>
          "first_name": <FIRST_NAME>
          ...
        }

## Partial Update User

Perform a partial update on user profile, if you are the user owner. Only fields specified in JSON PATCH request will be updated

**Permissions**: User Owner

**Endpoints**: <http://localhost:8000/api/users/PK/>

        PATCH REQUEST:
          Authorization: "Bearer <ACCESS_TOKEN>"
        PATCH DATA = {
          "email": "<EMAIL>",
          "password": "<PASSWORD>",
          (Any subset of fields to update)
          ...
        }

**Validation**:
- Individual Field Validation

## Full Update User

Essentially the same as “PARTIAL Update User” except you must specify all fields (including the password field)

**Permissions**: User Owner

**Endpoint**: <http://localhost:8000/api/users/PK/>

        PUT REQUEST:
          Authorization: "Bearer <ACCESS_TOKEN>"
        PATCH DATA = {
          "first_name": "<FIRST_NAME>",
          "last_name": "<LAST_NAME>",
          "email": "<EMAIL>",
          "password": "<PASSWORD>",
          ...
        }

**Validation**:
- Individual Field Validation


## List Users / User Filtering

Provide user filtering using query-params. Only public information is displayed

**Permissions**: Depends on request query-params
- To view all users: must be superuser
- To view all users in league: must be in league

**Endpoint**: <http://localhost:8000/api/users/QUERY-PARAMS>

**Query-Params**:

      /?league=<LEAGUE_ID>
      /?account_type=<ACCOUNT_TYPE>
      More options coming soon...

        GET REQUEST:
          Authorization: "Bearer <ACCESS_TOKEN>"

**Example Endpoints:**

<http://localhost:8000/api/users/>

- Returns a list of all users, returns validation error if not authorized as superuser

<http://localhost:8000/api/users/?account_type=ACCOUNT_TYPE>

- Returns a list of all users with given account type, returns validation error if not authorized as superuser

<http://localhost:8000/api/users/?league=PK/>

- Returns all users in league, returns validation error if not member of league

<http://localhost:8000/api/users/?leauge=PK&account_Type=ACCOUNT_TYPE>

- Returns all users in league and with account type, returns validation error if not member of league


## UserLeagueStatus Create

Create a UserLeagueStatus (typically used for Umpires/Managers to apply to leagues). The user can only create a UserLeagueStatus linked to their account, otherwise a validation error will be thrown. Returns the created UserLeagueStatus

**Permissions**: IsAuthenticated

**Endpoint**: <http://localhost:8000/api/user-league-status/>

        POST DATA = {
          "user": <USER_PK>,
          "league": <LEAGUE_PK>,
        }
        RESPONSE DATA = {
          "pk": <USER_LEAGUE_STATUS_PK>,
          "user": <USER_PK>,
          "league": <LEAGUE_PK>,
          "date_pending": <DEFAULT>,
          "date_joined": <DEFAULT>,
          "join_status": <DEFAULT>,
          "max_casts": <DEFAULT>
        }

**Validation**:
- User must be owned by current users, pk must exist
- Leauge pk must exist

## UserLeagueStatus Retrieve

**Permissions**: UserLeagueStatus owner

**Endpoint**: <http://localhost:8000/api/user-league-status/PK/>

        GET REQUEST:
          Authorization: "Bearer <ACCESS_TOKEN>"


## UserLeagueStatus Full/Partial Update

Follows standard HTTP verbs: PUT for full update, PATCH for partial update. Note: "full update" requires only all "required fields". User and League are read_only fields, cannot be updated here.

**Permissions**: UserLeagueStatus owner

**Endpoint**: <http://localhost:8000/api/user-league-status/PK/>

        PUT REQUEST = {
          (all required fields)
        }
        PATCH REQUEST = {
          (any subset of fields)
        }


## UserLeagueStatus Destroy

Destroy a model instance using the HTTP verb: DELETE

**Permissions**: UserLeagueStatus owner

**Endpoint**: <http://localhost:8000/api/user-league-status/PK/>


## UserLeagueStatus List / Filtering

Provide UserLeagueStatus in list format and provide filtering capability

**Permissions**: IsAuthenticated

**Endpoint**: <http://localhost:8000/api/user-league-status/>

**Query-Params**

        /?user=<USER_PK'>
