# Papertrail Heroku plugin

Extends `heroku` command-line app to display, tail, and search Heroku app and 
platform logs on [Papertrail](https://papertrailapp.com/).


## Installation

    $ heroku plugins:install https://github.com/papertrail/papertrail-heroku-plugin


## Usage

    $ heroku pt:logs [-t] [query]

      -t      # continually stream logs (tail)
      query   # Boolean search filter


## Examples

Add Papertrail's Heroku [log management addon](https://addons.heroku.com/papertrail) to your
app(s), then run `heroku pt:logs`. Examples:

    $ heroku pt:logs

Tail:

    $ heroku pt:logs -t

Specify a Heroku app name, tail, and show only `router` logs:

    $ heroku pt:logs --app wopr -t router

Create a shortcut:

    $ alias logs="heroku pt:logs --app wopr -t"


## Advanced Examples

To search for quoted phrases, enclose entire query in double quotes 
(consistent with other shell tools):

    $ heroku pt:logs "'Sent mail to' cron"
    $ heroku pt:logs -t "'status=50' OR 'Completed in'"

Use parenthesis and exclusion (-):

    $ heroku pt:logs --app wopr -t "'State changed' OR (router ('status=50' OR 'Error H'))"
    $ heroku pt:logs "router -'queue=0'"

More: [Search syntax](http://help.papertrailapp.com/kb/how-it-works/search-syntax)


## Tests

Prerequisites (gems):

* mocha
* papertrail-cli
* heroku

Run with:

    $ ruby test/papertrail_test.rb
