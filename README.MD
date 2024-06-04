Changes 06/04/24
* Fix for HTML_LinkToAddress from side/top menu options. I had added this but then had issues with some compatibilities... took HTML_LinkToAddress
  off of the side/top menu options but then added them back. Forgot to uncomment code I had commented out...

Changes 05/08/24
* Fix for when Control Web Properties won't assign (and you need to close the Window).

Changes 05/3/24
* Fix for ACTIVATE with many RESTRICTIONS causing weird java error.
* Latest Autodesign changes changes from Don.

Changes 04/22/24
* Fix for copy grid crash.

Changes 04/18/24
* Autodesign fixes/changes by Don.
* Fix for copy/paste radio group.

Changes 04/09/24
* Autodesign fixes/changes by Don.

Changes 03/28/24
* Autodesign fixes/changes by Don reported by Jeff.

Changes 02/27/24
* Fixed Jeff's issue where in Operation "Save As..." the Source File name was being truncated to 8.
* Fixed an error where "Save As" was giving an error when the Source/Target Source file were both "Java".

Changes 02/05/24
* Don's autodesign changes
* Updated AD_Base.7z

Changes 01/17/24
* Added AD_Base.7z (lplr for AD_Base), which is used by Don C's autodesign functionality.
* Generate jsp fix - give an error if a reusable Top/Side menu or actions does not exist (reported by David Loscutoff). Was getting "Invalid View" errors.

Changes 01/10/24
* Don C's updated autodesign code.
* Added the operation zGetAttributeDomainDataType( View, szEntityName, szAttributeName, StringBuilder szDomainType )
* On jsp generation, eliminated the "comment line" for controls with names. Now that all controls have a name/id, this is not needed. Example:
<% /* PushBtnSchedules:PushBtn */ %>
<% /* GroupBox30:GroupBox */ %>
* In the Dialog View->Control List... made a change that seems to fix the "Find by text/tag".


Changes 09/13/23
* Add class 'text-right' on variable header <th>, when we are generating bootstrap and the domain is a number. This was added to the normal
  <th> but not when it was a variable header <th> (the header text is coming from a mapped object).

Changes 08/22/23
* Took out adding Number to survey questions on survey questionaire. This now should be a part of the dQuestion derived attribute.

Changes 08/18/23
* Fix for HTML_LinkToAddress from side/top menu options (requested by Kindra).
* Moved Action termination actions around... put most used at top of list.
* More of Don's autodesign changes.

Changes 07/07/23
* Fixed error in GenJSP_MenuFunctionsRecurs that I introduced with last push, Exit Task termination.   (reported by Kindra)

Changes 06/15/23
* Fix for Copy Dialog Window (reported by Kindra)
* Change to Exit Task termination. If there is an operation or Next Dialog Window, we do not use the generic _OnUnload action.
  Otherwise, the action stays the same.
* More of Don's autodesign changes (not complete)

Changes 04/24/23
* Don's changes for autodesign and ER Import from database
* Added comment for action termination zWAB_StayOnWindowWebRefresh when there is javascript. The javascript
  is added to JSP action, not the js.
* Fix - Repeating Group did not have unique name for Grid.

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

