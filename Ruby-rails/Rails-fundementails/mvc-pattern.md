# The Model View Controller (MVC) Pattern

## Routes
Mathchers for the URL that is requested

```
GET "/about"

Takes the request "/about" and gives it to the about controller to handle

```

## Models

Database wrapper

User model
* query user records
* wrap individual records

this part of rails interacts with the database

## Views 

Your response body content 

Formats:
* HTML
* CSV
* PDF
* XML

this is hwat gets sent to the browsewr and displayed

## Controllers
Decide how to process a request and define a response