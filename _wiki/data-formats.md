---
title: Campaign Data Formats
---
Before reviewing data formats, please review the [[California Disclosure Laws for Campaign Finance|Campaign Finance]]. That document defines what must be reported, when, and through which forms. It also discusses the data tables and their expected interactions.

This document describes how to pull data from particular feeds, and reformat it into the data tables above.


## CalFormat

CalFormat is a specification that defines how any Agency may transmit campaign finance data to the Secretary of State. All jurisdictions use the same forms to collect campaign finance data. The only difference between jurisdictions is how (or if) they digitize the data and how they make it accessible to the public. From the calformat spec:

> In accordance with the requirements of SB 49, the Secretary of State (SOS) is required
to define a standardized record format or formats for transmission by the filing
community of data required to be filed electronically under SB 49. The SOS will accept
test files from vendors to ensure compliance and compatibility with these formats, and
publish a list of the certified vendors or other parties who have successfully filed test
reports with us.

The [documentation for CalFormat](http://campaignfinance.cdn.sos.ca.gov/calaccess-documentation.zip) is covered on the [Secretary of State's website](http://www.sos.ca.gov/campaign-lobbying/cal-access-resources/raw-data-campaign-finance-and-lobbying-activity/).

## Data formats

Different municipalities may have different formats, but there are two common formats across the state: NetFile and CalAccess.

### NetFile

* [Field definitions](https://data.sfgov.org/City-Management-and-Ethics/Campaign-Finance-Data-Key/wygs-cc76)
* @bcipolli: [Meeting notes](https://docs.google.com/document/d/114obh2uly004NwQ_hTKYQQiINr253Q4MV9biBl7JbuQ/edit) that will be used to fill this in--just adding here so I don't lose track.


### CalAccess

How to parse the Cal-Access database is also covered on the [Secretary of State's website](http://www.sos.ca.gov/campaign-lobbying/cal-access-resources/raw-data-campaign-finance-and-lobbying-activity/). Cal-Access raw data can be downloaded from the same page (about 800MB).

We currently use the [California Civic Data Coalition's Django code](https://github.com/california-civic-data-coalition/django-calaccess-raw-data) to download CalAccess data for 2014 and 2015 across the entire state.

We don't currently understand how to merge the data into a single, relevant table.
