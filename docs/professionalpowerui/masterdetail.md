# Generate a Master Detail

In this tutorial we generate screens based on two tables. One table for **activities** and one for **impedements**. After the creation of the two tables we are going to generate the screens:

The following 9 steps are described in detail below  

1. Start and activate IntelliJ (one time only)  
2. Create the two tables. (scripts are prepared)  
3. Generate Meta Data  
4. Generate application files  
5. Copy generated application files (to proper directories) 
6. Build and deploy to tomcat  
7. Copy generated menu part into application menu  
8. Add permissions for new menu  
9. Check the result  

## Start and activate IntelliJ
First we start IntelliJ. Intellij is the Integrated Development Environment (IDE). Of course you are free to use whichever IDE you prefer like Eclipse or NetBeans. 

>  * host ==> **Mac**, run command in **terminal**
>   * guest ==> **Windows**, run command in **MobaXerm terminal**  

* host  $`. ./intellij`
* guest $`intellij`

In the **intellij_complete_installation** click `OK`
![intellij_complete_installation](./../images/masterdetail/intellij_complete_installation.png)

In the **JetBrains Privacy Policy** click `Accept`
![jetbrains_privacy_policy](./../images/masterdetail/jetbrains_privacy_policy.png)

In the **Set The UI theme** click `Skipp All and Set Defaults`
![jetbrains_set_ui](./../images/masterdetail/jetbrains_set_ui.png)

Now you will see the **IntelliJ StartUp Screen** for a few seconds
![intellij_startup_screen](./../images/masterdetail/intellij_startup_screen.png)

In the **IntelliJ IDEA welcome screen** click `Import Project`
![intellij_welcome](./../images/masterdetail/intellij_welcome.png)

In the **Select directory with Maven pom file**  Select the following file  
`/home/vaizrdemo/workspaces/vaizrdemo/pom.xml`
![intellij_select_to_import](./../images/masterdetail/intellij_select_to_import.png)

In the **Import Project from Maven**  Click `Next`  
![intellij_import_project_maven](./../images/masterdetail/intellij_import_project_maven.png)

In the **Select Profiles**  Click `Next`  
![intellij_import_project3](./../images/masterdetail/intellij_import_project3.png)

In the **Select Maven Projects to Import**  Click `Next`  
![intellij_import_project4](./../images/masterdetail/intellij_import_project4.png)

In the **Please select project JDK** you have to execute the following steps  

1. Click on **<font color="green" size="10">+</font>**  the green plus sign in the left upper corner  
2. Click on **JDK**
3. Double-click on the **jvm** folder, this folder should open now  
![intellij_select_home_jdk1](./../images/masterdetail/intellij_select_home_jdk1.png)

4. In the open **jvm** folder select the first sub folder  
5. This is the **java-8-oracle** folder  
6. In the top field you should see the following selection `/usr/lib/jvm/java-8-0racle`  
7. At the bottom of **Select Home Directory for JDK**  Click `OK`  
![intellij_select_home_jdk2](./../images/masterdetail/intellij_select_home_jdk2.png)

In the **Import Project**  Click `Next`  
![intellij_inport_project5](./../images/masterdetail/intellij_inport_project5.png)

In the **Please enter a name to create a new IntelliJ IDEA project.**  Click `Finish`  
![intellij_inport_project6](./../images/masterdetail/intellij_inport_project6.png)

Finally De-Select **Show Tips on Startup**  
And click `Close`
![intellij_tip_of_the_day](./../images/masterdetail/intellij_tip_of_the_day.png)

**Once again these above steps you only have to do once.**

Now **wait** till indexing is **finished** You can see that at the bottom of the screen
![intellij_indexing_busy](./../images/masterdetail/intellij_indexing_busy.png)

You know when indexing is finished when you don't see it anymore
![intellij_indexing_finished](./../images/masterdetail/intellij_indexing_finished.png)


## Create the two tables  

For this tutorial we have to connect to a database. Implicit we connected to same database in the first tutorial. The credentials for this database are given below:

      username : vaizrdemo
      password : vaizrdemo
      database : vaizrdemo
      portnumber : vaizrdemo

There are several ways to connect to the database. Now we use the command line in IntelliJ.  
Put your mouse over the little dark square in the bottom left.
And leave your mouse there "**hoover**"
![intellij_start_other_commands](./../images/masterdetail/intellij_start_other_commands.png)

After two second a menu will come up. Clikc here on `terminal`
![intellij_go_to_terminal](./../images/masterdetail/intellij_go_to_terminal.png)

Now a terminal will open.  
Type in the following command `psql -U vaizrdemo`  
![intellij_run_postgresql](./../images/masterdetail/intellij_run_postgresql.png)

Please be aware that in this X-terminal IntelliJ the **command** is most times the **CTRL** button.  
Select the following **SQL statements**.  
Copy the **SQL statements**.  
And paste the **SQL statements** in the IntelliJ terminal with **CTRL V**  

```sql
DROP TABLE tsl_impedements
;
DROP TABLE tsl_activities
;

CREATE TABLE tsl_activities
(
    id serial
,   usr_id integer NOT NULL
,   description character varying(100) NOT NULL
,   creationtime date
)
;

ALTER TABLE tsl_activities
    OWNER to vaizrdemo
;

CREATE TABLE tsl_impedements
(
    id serial
,   act_id integer NOT NULL
,   description character varying(100) NOT NULL
)
;

ALTER TABLE tsl_impedements
    OWNER to vaizrdemo
;

ALTER TABLE tsl_activities ADD
  CONSTRAINT tsl_act_pk PRIMARY KEY (id)
;

ALTER TABLE tsl_activities
    ADD CONSTRAINT tsl_act_usr_fk FOREIGN KEY (usr_id)
    REFERENCES urp_users (id)
;

ALTER TABLE tsl_impedements ADD
  CONSTRAINT tsl_imp_pk PRIMARY KEY (id)
;

ALTER TABLE tsl_impedements
    ADD CONSTRAINT tsl_imp_act_fk FOREIGN KEY (act_id)
    REFERENCES tsl_activities (id)
;


```
After running the **SQL statements**. You should see the following screen.  
![intellij_run_postgresql_with_script](./../images/masterdetail/intellij_run_postgresql_with_script.png)

Now we start the real work in the IntelliJ IDEA
## Generate Meta Data  

If you open in the left pane the directory **tools**. You see a sub directory **generators**  
Right mouse click on the **Step01_GenerateMetaData.groovy** script.   
Select **Run 'Step01_GenerateMetaData'** in the DropDown menu and `Click`.  

![step01_generatemetadata](./../images/masterdetail/step01_generatemetadata.png)

After running the **Run 'Step01_GenerateMetaData'**. You should see the following screen.  
![step01_generatemetadata_result](./../images/masterdetail/step01_generatemetadata_result.png)

## Generate Application Files  
Right mouse click on the **Step02_GenerateApplicationFiles.groovy** script.   
Select **Run 'Step02_GenerateApplicationFiles'** in the DropDown menu and `Click`.  

![step02_generateapplicationfiles](./../images/masterdetail/step02_generateapplicationfiles.png)

After running the **Run 'Step02_GenerateApplicationFiles'**. You should see the following screen.  
![step02_generateapplicationfiles_result](./../images/masterdetail/step02_generateapplicationfiles_result.png)

## Copy Generated Files  
Right mouse click on the **Step03_CopyGeneratedFiles.groovy** script.   
Select **Run 'Step03_CopyGeneratedFiles'** in the DropDown menu and `Click`.  

![step03_copygeneratedfiles](./../images/masterdetail/step03_copygeneratedfiles.png)

After running the **Run 'Step03_CopyGeneratedFiles'**. You should see the following screen.  
![step03_copygeneratedfiles_result](./../images/masterdetail/step03_copygeneratedfiles_result.png)

## Build and Deploy to Tomcat  
Right mouse click on the **Step04_BuildDeploy2Tomcat.groovy** script.   
Select **Run 'Step04_BuildDeploy2Tomcat'** in the DropDown menu and `Click`. 

![step04_builddeploy2tomcat](./../images/masterdetail/step04_builddeploy2tomcat.png)

After running the **Run 'Step04_BuildDeploy2Tomcat'**. You should see the following screen.  
![step04_builddeploy2tomcat_result](./../images/masterdetail/step04_builddeploy2tomcat_result.png)

## Copy generated menu part into application menu  
Our build tasks in IntelliJ are finished and the last couple of tasks will be executed within the Vaizr Application. We have to make the new screens accessible in the menu of the Vaizr Application. This step conists of two actions.  
1. Add the new screen to the menu.  
2. Give permission on menu and screens to the proper role.  

First we will have look to the generated menu items. The generated menu can be found in `tools\generators\generated\navigation.json` If we open this file in IntelliJ we see the following structure.
![intellij_navigation_json](./../images/masterdetail/intellij_navigation_json.png)

The names are not yet pretty. The menu items are not encapsulated with a main menu and for permission we only see the splaceholder `<fill_in_permission>`. For your convienence a prettified menupart is added below:

```json
  ,
  {
    "name": "Master Detail Demo",
    "permission": "masterdetaildemo",
    "id": "thesprintlab_id",
    "items": [
      {
        "name": "Activities",
        "permission": "masterdetaildemo",
        "id": "nav_experimental_tsl_activities_id",
        "fn": "Assai.mainPageHandler.showSearchRecordsTab",
        "parameters": {
          "datasource": null,
          "recordType": "tsl_activities"
        },
        "disabled": false
      },
      {
        "name": "Impedements",
        "permission": "masterdetaildemo",
        "id": "nav_experimental_tsl_impedements_id",
        "fn": "Assai.mainPageHandler.showSearchRecordsTab",
        "parameters": {
          "datasource": null,
          "recordType": "tsl_impedements"
        },
        "disabled": false
      }
    ]
   }
```

This above menu part you are going to add to the menu of the vaizrdemo application.

Yuo can start a firefox browser in a separate window. 

>  * host ==> **Mac**, run command in **terminal**
>   * guest ==> **Windows**, run command in **MobaXerm terminal**  

* host  $`. ./firefox`
* guest $`firefox`

You can also run you preferred browser on your own desktop. Simply point to the following url `http://localhost:8080/vaizrdemo`  

You can login with:

username : `nanne`  
password : `nanneo`   

![vaizrdemo_login_nanne](./../images/masterdetail/vaizrdemo_login_nanne.png)

Go in the menu to **SBSGui parameters**.   
Click and go to **Multiline parameters**.   
Click again and in the right pane you see now a **Multiline parameters** search screen.  
Click `Search` . You now see 5 records. 

Double Click on **Main Menu**, the last record.

![vaizrdemo_menu_multiline_parameters](./../images/masterdetail/vaizrdemo_menu_multiline_parameters.png)

After double clicking on **Main Menu** you should see the following screen.

![vaizrdemo_change_multiline_parameters](./../images/masterdetail/vaizrdemo_change_multiline_parameters.png)

Scroll to the bottom and hit return **before** the **<font size="10">]</font>** the square closing bracket.  
You can see that the `Save` and `Undo` buttons are active now.

![vaizrdemo_change_multiline_parameters_modified](./../images/masterdetail/vaizrdemo_change_multiline_parameters_modified.png)

Copy the following json part just before the square bracket.

```json
  ,
  {
    "name": "Master Detail Demo",
    "permission": "masterdetaildemo",
    "id": "thesprintlab_id",
    "items": [
      {
        "name": "Activities",
        "permission": "masterdetaildemo",
        "id": "nav_experimental_tsl_activities_id",
        "fn": "Assai.mainPageHandler.showSearchRecordsTab",
        "parameters": {
          "datasource": null,
          "recordType": "tsl_activities"
        },
        "disabled": false
      },
      {
        "name": "Impedements",
        "permission": "masterdetaildemo",
        "id": "nav_experimental_tsl_impedements_id",
        "fn": "Assai.mainPageHandler.showSearchRecordsTab",
        "parameters": {
          "datasource": null,
          "recordType": "tsl_impedements"
        },
        "disabled": false
      }
    ]
   }
```

The screen should look like below :

![vaizrdemo_pasted_generated_menu](./../images/masterdetail/vaizrdemo_pasted_generated_menu.png)

You can check and prettify the menu in an <a href="http://jsonviewer.stack.hu/" target="_blank">online JSON viewer</a>. Just do **CTRL A** and **CTRL C** and paste the **menu** in the JSON viewer. You should see the following in the JSON Viewer. Here you have possibilities to format as well.

![online_json_viewer](./../images/masterdetail/online_json_viewer.png)

 If your JSON is not well formed you get the following error. You have to correct the error before saving the menu.

![online_json_error](./../images/masterdetail/online_json_error.png)

After saving the menu you can logoff and logon and check if the menu is still functioning. Now the final part. Adding the permission for the nem menu.

##Add permissions for new menu  

After logging on again with:  
username : `nanne`
password : `nanneo`

It is time to open the permissions which can be found in the **Users & Permissions** section.

![vaizr_permissions](./../images/masterdetail/vaizr_permissions.png)

In the permissions screen we add the **masterdetaildemo** permission. Click `Add` and after that fill in `masterdetaildemo` and click `Save`. After that click the `Add` button in the role permission sub part.

![vaizr_permissions_insert](./../images/masterdetail/vaizr_permissions_insert.png)

Next we are adding the role **SuperAdmin**. Just type `s` in the field.

![vaizr_permissions_roles](./../images/masterdetail/vaizr_permissions_roles.png)

After saving and closing the windows we log off and log on to check our work.

##Check the result  

If you see the following screen you succeeded in generating the master detail screen.

![vaizr_activities_impedements](./../images/masterdetail/vaizr_activities_impedements.png)