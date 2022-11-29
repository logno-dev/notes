#QA Data Entry

##Goal:
To create a simple way for techs to enter data revolving around the batched and finished products produced in Indio. To create a robust and intuitive way to review and report the data including remote access.

##Stretch Goal:
Create a smart hub for QA techs that guides daily tasks, including but not limited to calibration check reminders, viscosity testing, and shelf life testing.


##Requirements:
-Items should be easily located
-It should be extremely clear what item data is being entered for
-Data should be mutable within a reasonable time frame(?)
-Data edits after a certain time frame should preserve old data and require some form of accountability (e.g initial and comment)
-Techs should be able to click away from any given page without fear of losing data
-Lot data must be printable on a single sheet for filing purposes.

Discussion:
-Should software be hosted or local
  -Hosted 
    -Pros:
      -Accessible anywhere
      -Required Authentication for security
Updates and maintenance are seamless
Cons:
susceptible to breach
No internet, no software
Local
Pros:
Access to data will require the software to be installed locally(extra secure)
Continuous access even if internet is not available
Speed (No need to rely on stable internet)
Cons:
Data accessible only if client is installed
Updates are less seamless (not much of an issue though)
Traceability - Ideally, a finished product should be attached to a batched lot of white mass. Currently, if a single product type is stretched out among several tanks, it is ambiguous which tank a finished product came from. Do we want to push for better traceability? We do not timestamp or do extended codes on our date encoder, so even if we made a change to how we record the data, we would not be able to trace a cup plucked from the shelf to a specific tank batch.
If the above is dismissed, I’d push to remove the finished product from the lot data entry and record it in a distinct collection.
Who should have access to data
QA techs full access to entry and reports?
Some users limited access to only reports? (e.g Sherry)

Pricing:
Database: Depending on the package we use, the cost for hosting the DB could be negligible or it could cost ~$60/month.
Front-end hosting: Free to start, $20/month for the upgraded package (may never be necessary)
Other: Fixed computer for lab. It doesn’t need to be anything too powerful, so including monitor, mounting equipment, mouse and keyboard, ~ $400

Overall Pros and Cons (versus current pen and paper):
Pros:
Quality of life improvement for lab techs. Including more space to organize samples and no risk of paperwork being ruined by spill (which happens often)
Data instantly available for QA analysis
Ease of access for traceability
Clean, organized, and condensed paperwork for QA records.
Database is schemaless – meaning the data being loaded to the database is not required to follow a strict structure, so if fields are added or changed in the future, there is no need to restructure the database and the old data will not be affected.
Cons:
Software is software and it can have bugs. The database is separate from the front-end so the likelihood of a bug causing a loss or corruption of data is extremely unlikely.
Forms and inputs will be hard-coded so changes to the products or adding new product types will require updating the code. (In the future, I could potentially create an admin panel that would allow for a dynamic generation of product forms, but currently that’s a bit beyond my skill level)

…vs Google Sheets or Excel
Pros:
Since multiple people need to access this system to input data at several points in the process, using google forms would be a convoluted process that would require bouncing around several tabs and is prone to data being entered incorrectly with no easy way to correct it.
Leaving an open spreadsheet for techs to edit allows for tons of error inputs.
Data models are more complex than a simple relational database allows for. Using a simple relational database leads to tons of duplicate cells and unnecessary extra work for the techs
Creating an automated system for generating a daily report from a spreadsheet would be difficult to do and very easy to make mistakes.
Cons:
Google sheets and/or excel would require no costs for hosting.
Sheets and/or excel can be maintained by anyone at anytime
Sheets and/or excel could likely be deployed much sooner
	
