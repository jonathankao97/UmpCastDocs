# Installation

## Goal
Get a working copy of the UmpCast API source code in local production environment

## Clone the Project
        git clone https://github.com/UmpCast/UmpCastV2-Backend.git

## Install Dependencies
        python3 -m venv env/
        source env/bin/activate
        pip3 install -r requirements.txt

## Configure Environment Variables

UmpCast API expects the following environment variables to be defined.

- SECRET_KEY
- DEBUG
- ENGINE (DB Engine Type)
    - Currently, requires a PostgreSQL backend
- NAME (DB Name)
- SOCIAL_AUTH_FACEBOOK_KEY
- SOCIAL_AUTH_FACEBOOK_SECRET
- SOCIAL_AUTH_GOOGLE_OAUTH2_KEY
- SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET

## Migrate Database/Start Server
        python3 manage.py migrate
        python3 manage.py createsuperuser
        python3 manage.py runserver

## Create Social Auth Application for Social Login
1. Visit localhost:8000/admin and authenticate using superuser
2. Under Django OAuth Toolkit, create application
3. Select User (superuser created)
4. Leave client_id/client_secret (important for social login)
5. Select client_type: confidential
6. Select authorization_grant_type: resource owner password-based
7. Name: any name related to the application
