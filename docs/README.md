<!-- # Welcome to MkDocs

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files. -->

# Welcome to UmpCast API Docs!

## About
The UmpCast API was designed using the [Django Rest Framework](https://www.django-rest-framework.org/) to build an umpire management service for local little leagues

## How to use the Docs
The UmpCast API is partitioned into 4 "apps", each taking responsibility for a major aspect of the umpire management service

- **Users**: logic pertaining to user accounts
- **Leagues**: logic pertaining to leagues and their inherent structure. Includes league *Divisions*, and league umpiring *Roles*
- **Games**: logic pertaining to games, and applying to games. Includes game application *Posts* and *Applications* to those posts
- **Notifications**: logic pertaining to notification services provided by our app. Includes external email and text messaging notifications and internal feed notifications

Each of the 4 apps have related database models and API endpoints. Detailed information on specific models within an app will be found in the respective Model Dropdown in navigation. Similarly, detailed information on specific endpoints within an app will be found in the respective Endpoint Dropdown in navigation.

Lastly, there is Installation help for first-time users!
