# NFI-PM-Dashboard
----
## Goal

Create a dashboard which will concisely display the following information

1) Dry Van Trailers, Company Tractors and Owner Operator Tractors assigned to Profit Center 117
2) Rollerbed Equipment for Profit Centers 117 and 854 as rollerbed responsibility is shared between both profit centers.
3) Sort all equipment based on due percentage in decending order
4) A count of each asset type due for PM
5) Current trailer locations and user notes on steps taken to inspect trailers

Equipment becomes due and is inspected daily. As such the list needs to be dynamic by expanding and contracting without user intervention.

## Background

One of the primary goals within transportation is to ensure equipment is maintained and safe to use. Damaged or defective equipment can easily cause critical failures, which not only causes downtime and customer service failures, but can also result in major accidents which could injure truck drivers and the motorists they share the road with. In order to promote safe practices the <a href="https://www.transportation.gov/">Department of Transportation</a> regulates that all trailers and tractors must be inspected once per year for any worn or defective equipment by certified mechanics. National Freight takes this initiative a few steps further by having the following self imposed regulations on Pre-Maintanence (PM) Intervals.

| Equipment Type | PM Interval |
| -------------- | ------------------- |
| Dry Van Trailer | 6 Months |
| Rollerbed Trailer | 3 Months |
| Company Tractor | 6 Months |
| Owner Operator Tractor | 3 Months |

NFI Industries owns thousands of trailers so it is no small task to keep track of upcoming equipment maintenance especially as equipment can and do travel between Profit Centers (dispatch Terminals). The company supplies a bi-weekly report for trailers and tractors called the DAWG Report which lists every company asset which is over 85% due for PM but it is tedious and time consuming to find the relevant information for a specific profit center within the company. As such I created this report which automatically filters the relevent information for my profit center.

## Explanation

The dashboard was achieved using a three step process.
<img src="https://github.com/Ambisinisterr/NFI-PM-Dashboard/blob/main/assets/Dashboard%2006-26-22.png?raw=true"/>

### 1) Entering DAWG Reports
As the SQL servers are not directly accessible the DAWG report will need to be entered into the sheet manually. DAWG reports are sent via e-mail and only list one asset class per report. As such there is one sheet for each of the DAWG reports that users will need to update bi-weekly.

<img src="https://github.com/Ambisinisterr/NFI-PM-Dashboard/blob/main/assets/Trailer%20DAWG%2006-26-22.png?raw=true"/>

### 2) Filtering and Sorting
There are three hidden sheets to filter each of the asset classes accordinly and then sort them in decending order based on PM due percentage.

The following code filters the DAWG trailer data to only the trailers PC 117 is responsible for.
```
=FILTER(DAWGData!A2:I,DAWGData!A2:A="YES")
```
The following code sorts the filtered cells by PM percentage in decending order.
```
=SORT(M1:S30,S1:S30,0)
```
Similar code was used to filter Owner Op and Company Tractors.

### 3) Display Dashboard
Show the filtered and sorted information on the Dashboard Sheet. Use conditional formatting to ensure the page is easy to read and looks professional.

The following function will display all filtered and sorted trailer numbers, PM percent and trailer type filtering out blank rows.
```
=FILTER({'117 Trailer PM'!D1:D,'117 Trailer PM'!G1:G&"%",'117 Trailer PM'!E1:E},'117 Trailer PM'!D1:D<>"")
```

Similar formats were for the two tractor columns except it is filtering to only display tractors belonging to 117
```
#Owner Op
=FILTER({'117 Owner Op'!D1:D,'117 Owner Op'!H1:H,'117 Owner Op'!I1:I,'117 Owner Op'!G1:G},'117 Owner Op'!B1:B=117)
#Company tractors
=FILTER({'117 Tractor'!B1:B,'117 Tractor'!K1:K,'117 Tractor'!L1:L,'117 Tractor'!J1:J},'117 Tractor'!E1:E=117)
```

Additionally we want to allow users to add notes for each trailer on the list. In order to ensure the notes move as the lists change they have to be kept in a separate sheet. The bright side to this is that it allows the entire dashboard to be locked reducing the chances code sections could be broken. Trailers on this separate sheet are automatically flagged as being completed so users know they can be removed.

```
#Lookup matching trailer in the location and notes sheet, pull from the index offset of "Current Location," if null fill with a blank.
#Repeat for each trailer
=ARRAYFORMULA(IFNA(VLOOKUP(B5:B,'Location and Notes'!A2:D,3,0),""))

#Same as the above but pull at the offset for "Notes"
=ARRAYFORMULA(IFNA(VLOOKUP(B5:B,'Location and Notes'!A2:D,4,0),""))
```

<img src="https://github.com/Ambisinisterr/NFI-PM-Dashboard/blob/main/assets/LocationandNotes062622.png?raw=true"/>

## Finishing touches
The dashboard is fully functional at this point but not necessarily easy to understand at a glance. Conditional formatting was applied to each section so that the cells with text in them were automatically colored white, else they remain the default of light gray. Text was also set to wrap in the notes section in case notes became long. Unfortunately Google Sheets does not have a setting to add boders with conditional formatting.

# Possible Improvements
* Adding a button to pull data directly from the SQL servers up press. This will require permission and information from NFI's IT department.
* Adding custom code to workaround Google Sheets not supplying an auto-format for borders
