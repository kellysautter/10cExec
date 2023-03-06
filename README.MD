Changes 03/06/23
* Due to changes for autodesign, an error occurred that affected the rebuild of xods. This has been fixed.

Change 02/20/23
* On the Feb 3, 2023 commit, I committed a couple of files with an old date (tztedblo.xdl, tzopsigd.xwd and tzzolodd.xwd).
  This includes the newer files.
* This includes executables that were built on a different machine than previous versions. Hopefully should not
  cause any issues.

Changes 02/09/23
* Autodesign fixes.

Changes 02/03/23
* Incorporated Don C's Autodesign changes. Autodesign needs AD_Base.PWD in the c:\lplr directory.
* If you want to change AD_Base.PWD, you would need to download the lplr project CRMBase from git@github.com:kellysautter/CRMbase.git
  After making changes you copy AD_Base.PWD to c:\lplr.

Changes 01/30/23
* Made a change to jsp generation, for the reusable top menu, with horizontal menu actions and a banner.
* Changes made by Don C for Autodesign. This is code in progress and not complete. 

Changes 08/12/22

* Disable in Common was not working for MLEdit and for "Select Entity" combo box. This has been fixed.

Change 07/27/22
* For grids, when a fields was "", we were putting in &nbsp. Now keeps as "".

Changes 07/26/22
* Migration fix - copy over all source files (was not looping through all the source files for a dialog/object.
* Changed some tools naming to "Information Centric". Not sure this is permanent...
* JSP Generation - 
  took out Calendar size in grid
  MLEdit in grid

Changes 06/23/22
* Fixed issue where when migrating a Dialog with more than one source file, it didn't create all of the source files.
* Also, the vml files did not get copied during migration. Added this in. If the file is java or scala it is still incorrect. Need to change the
  sourcefile location in tzwdlgso.vml.

Changes 06/20/22
* Fix for MLEdit control in grid (previously only putting an Edit field).


Changes 06/01/22
* Now put back size on grid edit control

* KJS changes for Workstation Migration. More duplication elimination. Also allows user to start with moving a LOD like
  sHost.LOD and it will create the ER/PDG/LOD etc.
* Took "size=" off of grid edit control when bootstrap.
* Took "style=width:80px" off of grid calendar control when bootstrap.

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

