# NFI-PM-Dashboard
----

## Background

One of the primary goals within transportation is to ensure equipment is maintained and safe to use. Damaged or defective equipment can easily cause critical failures, which not only causes downtime and customer service failures, but can also result in major accidents which could injure truck drivers and the motorists they share the road with. In order to promote safe practices the <a href="https://www.transportation.gov/">Department of Transportation</a> regulates that all trailers and tractors must be inspected once per year for any worn or defective equipment by certified mechanics. National Freight takes this initiative a few steps further by having the following self imposed regulations on Pre-Maintanence (PM) Intervals.

| Equipment Type | PM Interval |
| -------------- | ------------------- |
| Dry Van Trailer | 6 Months |
| Rollerbed Trailer | 3 Months |
| Company Tractor | 6 Months |
| Owner Operator Tractor | 3 Months |

NFI Industries owns thousands of trailers so it is no small task to keep track of upcoming equipment maintenance especially as equipment can and do travel between Profit Centers (dispatch Terminals). The company supplies a bi-weekly report for trailers and tractors called the DAWG Report which lists every company asset which is over 85% due for PM but it is tedious and time consuming to find the relevant information for a specific profit center within the company. As such I created this report which automatically filters the relevent information for my profit center.

## Goal

Create a dashboard which will concisely display the following information

1) Only display Dry Van Trailers, Company Tractors and Owner Operator Tractors assigned to Profit Center 117
2) Only display Rollerbed Equipment for Profit Centers 117 and 854 as rollerbed responsibility is shared between both profit centers.
3) Sort all equipment based on due percentage in decending order
4) Display a count of each asset type due for PM
5) Current locations and notes on steps taken to inspect trailers

Equipment becomes due and is inspected daily. As such the list needs to be dynamic by expanding and contracting without user intervention.

## Explanation

The dashboard was achieved using a three step process. 

### DAWG Reports
As the SQL servers are not directly accessible the DAWG report will need to be entered into the sheet manually. DAWG reports are sent via e-mail and only list one asset class each. As such there is one sheet for each of the DAWG reports.

### Filtering
There are three hidden sheets to filter each of the asset classes accordinly and then sort them in decending order based on PM due percentage.

### Display
Show the filtered and sorted ifnormation on the Dashboard Sheet. Use conditional formatting to ensure the page is easy to read and looks professional.
