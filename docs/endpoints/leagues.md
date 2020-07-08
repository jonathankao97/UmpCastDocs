# Leagues Application Endpoints

## League Create

**Endpoint**: <http://localhost:8000/api/leagues/> (POST REQUEST)

## League Retrieve

Returns nested substructure

**Endpoint**: <http://localhost:8000/api/leagues/PK/> (GET REQUEST)


## League Full/Partial Update

**Endpoint**: <http://localhost:8000/api/leagues/PK/> (PUT or PATCH REQUEST)

## League Destroy

**Endpoint**: <http://localhost:8000/api/leagues/PK/> (DELETE REQUEST)


## League List

Returns a list of public league profiles. If user query-param is specified, returns all leagues associated to that user

**Endpoint** <http://localhost:8000/api/leagues/> (GET REQUEST)

**Query-Params**

        \?user=<USER_PK>


## Division Create

Note that Division only supports Create/Destroy functionality. Divisions should never be individually accessed or updated. See League

**Endpoint**: <http://localhost:8000/api/divisions/> (POST REQUEST)

## Division Destroy

**Endpoint**: <http://localhost:8000/api/divisions/PK/> (DELETE REQUEST)

## Role Create

Similar to Division. Only supports Create/Destroy functionality

**Endpoint**: <http://localhost:8000/api/roles/> (POST REQUEST)

## Role Destroy

**Endpoint**: <http://localhost:8000/api/roles/PK/> (DELETE REQUEST)


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
