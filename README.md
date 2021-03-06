changewithin is a simple script that pulls [daily changes](http://planet.openstreetmap.org/)
from OpenStreetMap with `requests`, parses them with `lxml`, finds the ones that are inside
of a GeoJSON shape, sorts out the ones that are buildings, and emails a set of users
with [mailgun](http://www.mailgun.com/).

The one file that will require editing is [users.json](https://github.com/osmlab/changewithin/blob/master/users.json). This is simply a list of email addresses to which the script will send the reports, in JSON format. The email templates for both html and text can be edited within script. The report itself contains a summary of changes, then lists each relevant changeset, its ID, and further details. These include the user who made the change and their comment, individual element IDs for building footprint and address changes that link to their history, and a map thumbnail that is centered on the location where the edits were made.

## Installation

Requires [wget](http://www.gnu.org/software/wget/).

for Mac use [homebrew](http://brew.sh/):

    brew install wget

for Ubuntu/Linux:

    apt-get install wget

Requires Python with [lxml](http://lxml.de/), [requests](http://docs.python-requests.org/),
[pystache](http://defunkt.io/pystache/), [PIL](http://effbot.org/imagingbook/),
and [ModestMaps](https://github.com/stamen/modestmaps-py).

Optionally [set up virtualenv](http://www.virtualenv.org/en/latest/#usage):

    virtualenv --no-site-packages venv-changewithin
    source venv-changewithin/bin/activate

Install libraries needed for fast XML processing and Python extensions.
For Ubuntu/Linux:

    apt-get install python-dev libxml2-dev libxslt1-dev

Install Python packages:
    
    pip install -r requirements.txt

## Running

    python changewithin.py

## Automating

Assuming the above installation, edit your [cron table](https://en.wikipedia.org/wiki/Cron) (`crontab -e`) to run the script once a day at 7:00am.

    0 7 * * * ~/path/to/changewithin/bin/python ~/path/to/changewithin/changewithin.py

