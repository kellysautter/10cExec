Changes 07/24/2025
* I needed to rebuild zeidon.xdm. For some reason "Show/Hide Group" web control property value was missing.

Changes 07/08/25
* Made the Global Operations window larger to give more space for the operation name. (Per Alan)
* I had to make a fix for the AutoIncludeComboBlank (because of errors with null values). But then nRegDemographics.jsp was too big ("exceeding the 65535 bytes limit").
  I added back needing the AutoIncludeComboBlank ini setting because I don't think we will use this code. But I don't want to delete it yet.

Changes 06/20/25
* I took off using the zeidon.ini AutoIncludeComboBlank=Y for the Auto Include/Source Entity because I think we will always want it.
* But I copied that zip file to 10cExecHFI.zip for now so that GMC will not get messed up before our monthly install. Would want to test a little further at GMC...

Changes 06/19/25
* I had to re-save TZPNTRAD.PWD/XWD. We were getting weird dialog errors (with  ActMapLOD_Entity). I think this has to do with when my "Dialog" tool was pointing to "10d" and not using %kzv (which was pointing to "10c"). 

Changes 06/17/25
* For the below Auto Include change, I needed to add a fix because of how we position on the correct entity in DoInputMapping. This is slightly different based on
  whether or not the original map list has a blank entry or not.

Changes 06/13/25
* Instead of the change I made on 06/11 for "Set Foreign Key/Select Source..", I made a change to the Auto Include to NOT add a blank to the combo if a blank (as the
  first entry) already exists. For now this requires the zeidon.ini setting:
  AutoIncludeComboBlank=Y

Changes 06/11/25
* Took off 22 LOD operation limit (it's 32). I think there might be an issue when the LOD name is long but I haven't come across it yet so will try (per Alan).

Changes 06/11/25
// I had added the below code, but realized it doesn't work (which is why we hadn't done it), might still try to see if I can get it to work so I won't take out
// since it needs an ini addition so shouldn't hurt any project.
* When a combo box is "Set Foreign Key/Select Source Entity Only", a blank entry was not being added in the jsp (Domain/Auto Include adds a blank). This is an 
  inconsistency so we now have a blank entry automatically created for these combo boxes. 
  Because on previous applications, we usually add a blank through VML, and this would then have two blanks, I added a tools zeidon.ini setting for this:
  SourceEntityComboBlank=Y

Changes 06/03/25
* Fix for postgres sql and MM tables in the DDL creation. FK Field type was not being created.

Changes 05/29/25
* A change has been made for when we do not want users to be able to log into an application on more than one tab in a 
  browser (zeidon.ini "NoMonitorTaskLogout=N"). In order for this to work, a link needs to be made in the loggedintotask.jsp 
  something like the following which sends the user to the logout.jsp page:
  <p align="center">If you believe you have received this message in error, <a href="logout.jsp">click here</a> to end your previous session.</p>

  And the following needs to be added to the logout.jsp (to create a new SESSIONID):
session.invalidate();

Cookie killSessionCookie = new Cookie("JSESSIONID", null);
killSessionCookie.setMaxAge(0);
killSessionCookie.setPath("/"); 
killSessionCookie.setDomain(request.getServerName());
response.addCookie(killSessionCookie);

* For our language translation with picklist (table) domains, a separate file was needed "jspWebUtilsLang.java" in the LPLR, in order to       
  populate the combo boxes for those domains on the jsp page (call made to jspWebUtilsLang.getTableDomainValuesLanguage()).
  I have taken that out of the jsp generation and we now always call jspWebUtils.getTableDomainValues() (this was the original
  call for domain picklists). Code has been added to our LPLR specific domains (like DynamicTableDomainWContextAndLang.java) to
  to use our language translation code when jspWebUtilsLang.getTableDomainValuesLanguage() is called.

Changes 05/01/25
* An error was introduced on a grid when the column was a "select" checkbox column, where there is no heading for the column (this puts a checkbox 
  in the heading and "selects all" when clicked). After clicking, the page blanks out.
  This is only when the grid is of type "Sort Underlying View" and is fixed.

Changes 04/29/25
* Not sure why... but Checkbox Update did not have the two css fields (checkbox/checkbox label). Resaved tzpntcad.pwd, now visible.

Changes 04/21/25
* To the Technical Environment, added a field "Schema Name" for the Data Source. For Postgres, a schema name is needed when correctly running the "Sync DDL".
* Previously when running the "Sync DDL", the database UserID/Password was retrieved from the "[WorkStation]" portion of the zeidon.ini, which was a problem when
  different LPLRs have different user ids/passwords. Now when looking for this, it first looks to see if the "[App.xxx]" has a UserID/Password definied. If so, that
  is used. If not, the workstation one is used. Per Jeff Beam
* When creating tables for Postgres, the ID for an entity is now being created as:
  int4 GENERATED BY DEFAULT AS IDENTITY( INCREMENT BY 1 MINVALUE 1 MAXVALUE 2147483647 START 1 CACHE 1 NO CYCLE) NOT NULL
  This is because of "autoincrement" from the database. Per Jeff Beam
  CURRENTLY - this is only working for all Postgres Data Sources, not just "PostgresSQL AutoIncrement". This is for HFI which I believe is currently the only
  Company using Postgres. This needs to change so that both types of Postgres can work.
* In the Editor/Entity Insert - Added Domain Name/Attribute Description to the Attribute list. Per Justin Schmitz.

Changes 03/31/25
* For the "grid header vml sort", I had to fix the hard coding of "PersonList2". Oops!
 
Changes 03/25/25
* Added Attribute description field to Object Maintenance "Entity Attribute List", "View->Object Entity List" 

Changes 03/18/25
* Fixes/Changes for grid header sort. Now, grid must have radio button "Sort Underlying View" selected to get the OrderEntityForView to occur when header is clicked.
* Fix so header for subentity will sort correctly.
* If grid is a DataTable (bootstrap). Then we do not add the .\images\arrow_up/down.png because we bootstrap puts that in.
  ** Note - if the grid is a DataTable and "Sort Underlying View" is selected, there needs to be a custom data-table .js file to disable the bootstrap ordering. Like the following.
{
    const vmlSortTables = $(".data-table-vmlkelly-sort");
    // Set up VML sort tables as DataTables with a custom onclick event for column headers
    vmlSortTables.DataTable({
        // Disable the default client-side sorting
        "ordering": false,
    })
}

Changes 03/12/25
* More changes for grid header sort, added arrow up/down on field being sorted. Per David Loscutoff.

Changes 03/07/25
* Added the web property 'Show/Hide Group Box' so that a group box that is not 'Toggle' can be excluded from being created on a page. Per David Loscutoff.
  When SetCtrlState is used... with this property, the control is not build on the jsp page. Without it, the control is "hidden". Important difference if hiding something like SSN.

Changes 03/06/25
* Trying new code for grid header sort, that sorts the view not just the table entries. Per David Loscutoff.

Changes 02/21/25
* Fix for grid control CSS error, reported by Dave Loscutoff.

Changes 02/17/25
* Don's latest autodesign changes.
* New AD_Base.zip the lplr used by autodesign.

Changes 02/10/25
* Fixed jsp generation error where a GridComboCtl's mapping wasn't creating a View variable in DoInputMapping.

Changes 01/14/25
* Added two fields to Control 
  CSS_Class2
  WebHTML5Attribute2
  This is so that on a checkbox we can have a css/html5 for both the checkbox <input> and the checkbox text <span>.
* Latest updates for autodesign from Don C.

Changes 01/09/25
* Changed tzlodopr.h #define WHERE_ARRAY_SIZE 30 to #define WHERE_ARRAY_SIZE 100 (long WHERE clauses were causing an error)

Changes 10/08/24
* Added *.xrp files to this zip

Changes 08/29/24
* Don C's changes to "Merge" and "Autodesign"
* Fix to file download processing (also Jasper downloads) where tomcat console displayed the following error:
  "****  Data ERROR within <form> ***** getOutputStream() has already been called for this response" (Thanks Kindra!)

Change 07/18/24
* Don C's fixes for Workstation "Merge" processing 

Changes 07/10/24
* Took out generated js code that included "eval(...". The .focus() can easily be created using javascript in an action.
  This was taken out becuase eval is not secure and creates issues when using <meta http-equiv="Content-Security-Policy".

Changes 06/26/24
* Don's changes for Merge and Migrate.
* Fix in generation of jsp (problem with the logout not going to the logout.jsp on generate for all dialogs).

Changes 06/05/24
* Forgot to uncomment a line I had commented out when fixing the 05/08/24 issue (with web properties), so all operations
  were being displayed in the operation drop down on the Update Action window.

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

