---
title: Types of Committees
---
(Almost) everything you need to know about campaign finance data in California

## Types of Committees

Every ballot measure will have committees associated with it. The name of a committee should indicate its type. You can also look at Form 410, the Statement of Organization, which describes the committee's purpose and names its treasurer.

* **Candidate Controlled Committee** - At the very least, a person running for office will have one Candidate Controlled Committee, unless that candidate does not plan to spend or raise more than $1,000 total. Each candidate has one bank account where money can be spent for a campaign. Even money from the candidates themselves must be contributed into this bank account before being spent.

* **Primarily Formed Committees** - Committees formed, either in support of or opposed to particular candidates, can accept contributions to spend on a campaign. These organizations can be short-lived and specific to particular campaigns, but must declare a candidate affiliation (and whether supporting or opposing).

* **General Purpose Committees** - These can also spend money in support of or opposition to candidates and ballot measures.

* **Ballot Measure Committee** - Any person or group receiving contributions for the qualification, passage or defeat of a ballot measure (such as Props, not candidates). A Primarily Formed Ballot Measure Committee runs the "principal campaign" for or against one or more Props. A General Purpose Ballot Measure Committee is more often formed around "issues" and may support or oppose Props in more than one state or election.


## Reporting Contributions and Expenditures

***All contributions must be reported publicly.*** The most comprehensive report for contributions and expenditures is the Form 460. However, the timing of what is reported when, and whether data is reported once or multiple times, depends on the specific campaign laws.

Information here was gleaned from the [California Fair Political Practices Commission](http://www.fppc.ca.gov/) [manual for campaign Finance](http://www.fppc.ca.gov/content/dam/fppc/NS-Documents/TAD/Campaign%20Manuals/Final%20Manual%202%20March%202015.pdf) (published in March, 2015) and the [San Diego Ethic Commission](http://www.sandiego.gov/ethics/) [manual for campaigns](http://www.sandiego.gov/ethics/pdf/manuals/candidatemanual_150302.pdf).

Form | Purpose | Polling Frequency | Contribution Level
-----|---------|-------------------|-------------------
460 Schedule A | Monetary contributions to committee | Semi-annually, or according to pre-election schedule | >= $100
460 Schedule C | Non-monetary (services/goods) contributions to committee | Semi-annually, or according to pre-election schedule | >= $100
497 | Contributions to committee | Within 24 hours, if received within 90 days of the election | >= $1000
496 | Independent expenditures | Within 24 hours, if spent within 90 days of the election | >= $1000
460 Schedule D | Committee Expenditures | Semi-annually, or according to pre-election schedule | >= $100

To get a comprehensive total of the amount of money raised for any ballot measure, you must include:
* Form 460, Schedules A (monetary contributions) and C (nonmonetary contributions), for all Primarily Formed and Candidate Controlled committees
* Form 497, beginning from the ending period of the last Form 460 that was filed, for all Primarily Formed and Candidate Controlled committees
* Form 496, only expenses in support, only from committees that are NOT the Primarily Formed or Candidate Controlled committees, and only those beginning from the ending period of the last Form 460 that was filed

NOTE: 
* **Do NOT need to use** Form 460, Schedule D, only expenses in support, and only from committees that are NOT the Primarily Formed or Candidate Controlled committees. This data will come in via Form 496, and only appears here, so safer to use Form 496 and ignore Form 460 Schedule D
* You should remove, **but probably don't need to**, Form 460, Schedule A, and form 497, when a contribution is made from one Primarily Formed or Candidate Controlled committee to another Primarily Formed or Candidate Controlled committee in support of the same candidate. These could be thought of as "internal transfers," and would be duplicative to include.


## Complexities

### Some data overlap in time

Form 497 and Form 460 Schedules A & C overlap; this requires 497 data to be removed when overlapping 460 data arrives:
  * Contributions $1,000 or greater are reported via 497 within 24 hours.
  * These same contributions are re-reported via 460 A&C ~every 3 months during a campaign (6 months outside a campaign), along with all other contributions $100 or greater and a lump sum for unitemized contributions less than $100.

### Some data should not be included.

Some items function as "transfers" and should be removed:
  * Items in 497 & 460 Schedule A can go between known entities for/against a campaign.


### Local Laws may complexify reporting.

To add complexity to things, local municipalities can add their own reporting requirements.

For example, during elections, San Diego requires an additional form 497 report to be filed on the Friday before the election, covering through the Wednesday before the election (presumably to account for any last-minute money that may come in, and avoid undisclosed last-minute floods to campaigns). This is outside of any regular reporting on Forms 460 and 497. Like other 497 reports, that money will be accounted for in a later form 460 report, but it needs to be published immediately for timely disclosure (and then purged later).


## An example timeline

[to be updated by @andrell81]

Taken from [San Diego's Candidate Manual](http://www.sandiego.gov/ethics/pdf/manuals/candidatemanual_150302.pdf)

>For the June 7, 2016, primary election and the November 8, 2016, general election, the most relevant filing deadlines (and applicable reporting periods) are set forth below.

>The candidate’s campaign activities in 2015 are reported on semi-annual campaign statements, as follows:

Period | Form | Reporting Period | Filing Deadline
-------|------|------------------|----------------
1st semi-annual period | (Form 460) | 1/1/15 – 6/30/15 | 7/31/15
2nd semi-annual period (Form 460) | 7/1/15 – 12/31/15 | 2/1/16

>In 2016, candidates participating in the primary election must file three pre-election reports before the primary election, and a semi-annual report after the election, as follows:

Period | Form | Reporting Period | Filing Deadline
-------|------|------------------|----------------
1st pre-election period | (Form 460) | 1/1/16 – 3/17/16 | 3/22/16
2nd pre-election period | (Form 460) | 3/18/16 – 5/21/16 | 5/26/16
3rd pre-election period* | (Form 497) | 5/22/16 – 6/1/16 | 6/3/16
1st semi-annual period | (Form 460) | 5/22/16 | 8/1/16

** * = San Diego specific **



## Ideas for data tables & data management

Some data can be scraped from [[Netfile/CalAccess data feeds|Campaign Data Formats]], while others must be entered manually.

Data Type | How is Data Entered? | Foreign Keys/Additional Fields
------|----------------------|-------------
Candidates / Ballot measures | Manually | None
Committees | ID & name(s) is found automatically from data feeds; candidate affiliation probably needs to be entered manually. | Candidate_ID
Contributions For | Automatically, from Forms 460 A&C, 497, 496/460D when in support of candidate. | Committee_ID, ReportingPeriod_ID, FormType
Contributions Against | Automatically, from Forms 496/460D when in opposition of candidate. | Committee_ID, Candidate_ID, ReportingPeriod_ID, FormType, support/opposition
Reporting Period | Manually at first (to be able to classify latest 497 data as campaign or not-campaign), then matched by Form 460 data (which specifies start/end period) | None


This could be handled by five tables:
* **Candidates**: ID (arbitrary), Name, Description
* **Committees**: ID (taken from form reports) canonical name (most frequently cited name), and with foreign key to Candidates/ID
* **Committee Aliases**, with Committee_ID, Alias (text), and # times the alias is referenced in the forms.
* **Contributions**, with ID, Committee_ID, Candidate_ID, Support/Opposition, Form, Date Entered, Reporting Period, Amount, Notes
* **ReportingPeriod** (corresponds to non-overlapping form 460 periods): StartDate, EndDate, Purpose (Election vs. Non-Election)

Note that additional fields must be entered, to indicate municipality information. They are excluded here for simplicity's sake.


## Open questions

* Do we want to deal with loans?
* Will there be overlap between NetFile & CalAccess data feeds?
