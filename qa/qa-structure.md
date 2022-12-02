# Top bar with main navigation

***

## Dashboard
Landing page with quick charts and reminders of things to complete.
Quick links to todays production entry page

***

## Entry
This pages navigation is very important and should intuitively guide the user to the proper item that needs data input.

* This page will have 2 tabs, one for batching and one for finished product.
* A column on the left will display a list of the most recent n number of items.

### Batching Tab
* "Add new lot" button stretches accross the entire screen
  * Button mutates to a form for basic product info to create new lot including: date(autofill to current date), tank number (fermentation tank for fermented foods), product type
* below is split into two colums, one listing recent lots
* Second column is where data is entered
  * Fermented items will have fields for UHT processing and innoculation, raw batching, fermentation checks, and break info
  * ESL items will include only raw batching info
  * Cheese will include all data collected by QA team

### Finished Product Tab
* "Add new item" button will stretch accross the screen
  * Button mutates to a form for basic product info including: product type, flavor, size, enjoy by date, label code
* When a new item is added, a grid will populate based on the product type with the required fields.
* Each product will start with one row of empty inputs and a button to add aditional rows as needed.
* All finished products for a given date will be recorded on the same page

***

## Reports
This will be a hub for printing all needed reports for a given day

### Left Column
Reports will be listed in a left column. Reports that have not been printed will apear at the top with some sort of indicator stating that the following reports are not finalized. In the report view, there will be an option to finalize the report, this will make it so that the data cannot be changed within the Entry page. The report can then be printed and submit for filing. Past reports will be listed below with an option to search for a specific date. Editing a finalized report will be possible but it will require a comment and a duplicate of the data will be stored in a different collection. 

### Right Column
Actual report will be displayed here with an option to print

***

## Analysis
This will be a page featuring several methods of analyzing the data input.

* Simple spreadsheets can be generated singling out specific attributes on certain flavors.
* Various types of graphs can be generated to analyze trend lines
