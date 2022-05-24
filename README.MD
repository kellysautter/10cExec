Change 05/24/22

* Some changes had been made for bootstrap main navigation menu when there was a banner specified (this was for
  Jeff nmmftm) and this messed up the top menu in nmm (where no banner was specified). The top menu for bootstrap
  that is horizontal AND no specified banner, should now generate as it had originally.

Change 05/23/22

* If generating jsp using Bootstrap and a field in a grid has a domain type of  "Number" or "Decimal" AND there is not CSS with "text-left" in it, 
  we add the class of "text-right" to right align fields.

* This also contains some code by Don C. for LOD attribute/derived rules but that code is not yet completed.

Changes made to 10c (update on 04/26/22):

* Kindra migraged from nazsis to iboereports. Duplicate domains were created. I added a button "Delete Duplicates" to the domain list. Also, when deleting
  a single domain, I took out the error that would not allow save if there were duplicate domain names.

Changes made to 10c (update on 04/03/22):

* I had made a generation change for Jeff on 08/27/21 for nmmftm where he wants top menu across but had a top banner to include. That messed up nmm where there
  is no top banner. Made changes so if there is no top banner, we create code like originally.
* There are changes in this from Don. He has made changes to the ER Merge process (for Entity only). This is partially for his demo purposes.

* Changed variable header to always create <th> even if blank. There had been a difference between <th> created and <td> created. Now they are the same.

Changes made to 10c (update on 04/08/22):

* Changed variable header to always create <th> even if blank. There had been a difference between <th> created and <td> created. Now they are the same.

Changes made to 10c (update on 02/16/22):

* Change to jsp generation. If generating boostrap, for the <nav sidebar, add class "contentExists" if there are menu options in the sidebar. This is used for showing/hiding sidebar.
* Jsp generation, add quotes around filename="filename" on file download because of issues in Chrome with files containing a comman in the filename.
* Widen the Global Operation operation list window.

