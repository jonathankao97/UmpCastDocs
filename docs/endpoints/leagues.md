# Leagues Application Endpoints

## League Create

**Permissions**: Is Manager

**Endpoint**: <http://localhost:8000/api/leagues/>


        POST DATA = {
          "title": "<LEAGUE_NAME>"
        }


## League Retrieve

Returns nested substructure of league including divisions and roles

**Permissions**: Is League Owner

**Endpoint**: <http://localhost:8000/api/leagues/PK/>

        GET REQUEST:
          Authorization: "Bearer <ACCESS_TOKEN>"


## League Full/Partial Update

**Permissions**: Is League Owner

**Endpoint**: <http://localhost:8000/api/leagues/PK/>

        PUT/PATCH DATA = {
          "title": "<UPDATED_TITLE>"
          ...
        }

## League Destroy

**Permissions**: Is League Owner

**Endpoint**: <http://localhost:8000/api/leagues/PK/>

        DELETE REQUEST:
          Authorization: "Bearer <ACCESS_TOKEN>"

## League List

Returns a list of public (not private) league profiles. If user query-param is specified, returns all leagues associated to that user

**Permissions**: Is Umpire Owner

**Endpoint** <http://localhost:8000/api/leagues/>

        GET REQUEST:
          Authorization: "Bearer <ACCESS_TOKEN>"

**Query-Params**

        \?user=<USER_PK>


## Division Create

Note that Division only supports Create/Destroy functionality. Only add other functionality if necessary. Additional validation requirements in serializer level

**Permissions**: Is Manager

**Endpoint**: <http://localhost:8000/api/divisions/>

        POST DATA = {
          "title": <DIVISION_TITLE>,
          "league": <LEAGUE_PK>
        }

## Division Destroy

**Permissions**: Is Division Owner

**Endpoint**: <http://localhost:8000/api/divisions/PK/>


        DELETE REQUEST:
          Authorization: "Bearer <ACCESS_TOKEN>"



## Role Create

Similar to Division. Only supports Create/Destroy functionality. Additional validation requirements in serializer level

**Permissions**: Is Manager

**Endpoint**: <http://localhost:8000/api/roles/>

        POST DATA = {
          "title": <ROLE_TITLE>,
          "division": <DIVISION_PK>
        }

## Role Destroy

**Permissions**: Is Division Owner

**Endpoint**: <http://localhost:8000/api/roles/PK/>

        DELETE REQUEST:
          Authorization: "Bearer <ACCESS_TOKEN>"



## ApplyLeagueCode Create

**Endpoint** <http://localhost:8000/api/apply-league-code/> (POST REQUEST)

## ApplyLeagueCode Retrieve

**Endpoint** <http://localhost:8000/api/apply-league-code/PK/> (GET REQUEST)

## ApplyLeagueCode Update/Partial Update

**Endpoint** <http://localhost:8000/api/apply-league-code/PK> (PUT or PATCH REQUEST)

## ApplyLeagueCode Destroy

**Endpoint** <http://localhost:8000/api/apply-league-code/PK>  (DELETE REQUEST)

## ApplyLeague Code List

**Endpoint** <http://localhost:8000/api/apply-league-code/> (GET REQUEST)

**Query-Params**

        \?league=<LEAGUE_PK>
