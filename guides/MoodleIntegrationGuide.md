[Home](https://equella.github.io/)

# Moodle Configuration Guide  


* [Integration overview](#integration-overview)
* [Open source](#open-source)
* [Prerequisites](#prerequisites)
* [Integration procedure](#integration-procedure)
* [Configure EQUELLA](#configure-equella)
* [Configure Moodle](#configure-moodle)
* [Enable Moodle drag and drop auto add to EQUELLA function](#enable-moodle-drag-and-drop-auto-add-to-equella-function)
* [QTI 2.1 with Moodle EQUELLA integrations](#qti-2.1-with-moodle-equella-integrations)  
* [Troubleshoot an unsuccessful integration](#troubleshoot-an-unsuccessful-integration)
* [Upgrade the EQUELLA Moodle Module](#upgrade-the-equella-moodle-module)
* [Viewing the EQUELLA Moodle Module change log](#viewing-the-equella-moodle-module-change-log)



## Integration overview 

EQUELLA integrates easily with Moodle™ by using the EQUELLA Moodle Module to create a seamless system for users. Additionally the EQUELLA Shared Secret functionality provides a single sign-on for users.

The purpose of this guide is to provide system administrators with an understanding of the EQUELLA Moodle integration process to enable successful integration. 

Please note that this guide has been developed for Moodle version 2.9 and, as such, may differ in appearance to your own installation.


## Open source  

he Moodle module, blocks and legacy repository plug-in are available under the GPLv3 license. The source code for these projects can be found at <https://github.com/equella/>.

## Prerequisites 

To successfully complete this installation the system administrator will require:
* sufficient privileges to access the Moodle system integration functionality;
* sufficient privileges to access the EQUELLA User Management functionality; and
* privileges to unzip and create files on the Moodle file system.

#### System prerequisites for integration
•  EQUELLA opens source and Moodle version 2.6, 2.7 or 2.8 must be installed and running. Further information on installing EQUELLA is provided in the EQUELLA Installation and Administration Guide.
•  Ensure the time settings of the servers are set correctly, including DST, for the relevant time zone.
•  To access the EQUELLA Dashboard page at least one course must have been created in Moodle. Refer to the Moodle documentation for more information. 


## Integration procedure  

EQUELLA Moodle integration can be broken into the following steps:
1.  Configure and enable the LTI consumer and shared secret in the EQUELLA User Management tool.
2.  Download the Moodle Module from the EQUELLA Institution Manager.
3.  Install the EQUELLA Moodle Module to the Moodle directory.
4.  Activate the EQUELLA Resource Module in Moodle.
5.  Test the installation.
 

## Configure EQUELLA  
This section describes the required configuration changes to EQUELLA to support a seamless integration. To achieve this, an EQUELLA LTI Consumer needs to be registered, along with a Shared Secret configuration.
Register an LTI consumer

LTI consumer client registrations are registered from the Settings page in EQUELLA.

To create a new LTI consumer
1.  Select Settings from the navigation menu, and either type LTI in the filter box, then select LTI consumers from the results or scroll down to LTI consumers on the Settings list.
2. Select the Create new LTI consumer link to open the Create new LTI consumer page. 
3. Enter a Title (e.g. Moodle LTI) and a Description (optional).
4.  A default Consumer key displays. This can be changed as desired (e.g. moodleint). Take note as the Consumer key is entered in Moodle during integration configuration.
5.  A default Consumer secret displays. This can be changed as desired. Take note as the Client secret is entered in Moodle during integration configuration.

Other options can be enabled as required. 

### LTI/LIS Role Mappings
When logging into Moodle, users are assigned a Moodle role which can be Teacher or another role. Moodle’s Teacher role is translated as Instructor for LTI purposes, and all other roles as Other. LTI ‘Instructor’ and ‘Other’ roles need to be mapped to the relevant EQUELLA roles for EQUELLA permissions to apply. Additionally, it is wise to map Unknown roles that may be sent to EQUELLA. This is done from the LTI/LIS Role Mappings section of the Add new LTI consumer or Edit LTI consumer pages. 

The LTI/LIS Role Mappings section has three areas:
* Instructor role – map the Moodle ‘Teacher’ role to EQUELLA role/s.
* Other roles –this area is used to map all other roles that might be used in the integration. A list of the standard LTI/LIS roles is supplied, of which ‘Other’ is one. 
* Unknown roles – use this area to select the EQUELLA roles to default to when an unknown role is sent to EQUELLA. 

#### Mapping the Instructor and Unknown roles
In the Instructor and Unknown roles fields, the Add roles link is used to select the EQUELLA roles to be used in the mappings. An example using the Instructor role is shown below:

To map to EQUELLA role/s
1.  Click the Add roles link under the Instructor role field. The Select role(s) dialog displays. 
2.  Enter a search query then click Search. Matching results display. 
3.  Select the required role/s, then click Select these roles. The mapping/s displays in the Instructor role field. 
4. Select the Add roles link to add more mappings.

#### Mapping the ‘Other’ role
The Other roles section is used to map LTI/LIS standard roles (including the role ‘Other’ which is used in the Moodle integration) to EQUELLA roles. 

To map the ‘Other’ role
1.  In the Other roles area, start typing the required LTI/LIS role (Other) in the Enter LTI/LIS role field. A list of all the standard LTI/LIS roles displays in a drop-down list.
2.  Select Other from the drop-down list.
3.  Click the Add roles link next to the selected LTI/LIS role.  The Select role(s) dialog displays. 
4.  Enter a search query then click Search. Matching results display.
5. Select the required role/s, then click Select these roles . The mapping/s displays in the Other roles field. 
6. To add further EQUELLA roles to ‘Other’ roles that have existing mappings or to add another LTI/LIS role mapping, repeat steps 1 to 5.

### Configure a shared secret
Shared secrets are configured in the EQUELLA Administration Console.

To open the Administration Console
1.  Open a browser and enter your EQUELLA URL (e.g. ‘<http://equella.myequellainstitution.edu>’).
2.  Log in to EQUELLA as an administrator, select Settings then Administration console. 
3. The Administration console displays. Select User Management to display a list of plug-ins. 
4.  Highlight the Shared Secrets user management plug-in, then click Configure. The Shared Secrets dialog displays. 
5.  Click + Add  to create a new shared secret. The Shared Secrets dialog now displays a new shared secret named ‘DEFAULT’ in the left-hand pane, and the configuration elements to the right of the pane. 
6.  Enter a unique Identifier (ID) (e.g. moodle). 
7.  Enter a shared secret (e.g. mS3cr3t). The secret may be any combination of characters and numbers, but strings longer than eight characters consisting of upper and lower case alphanumeric characters are recommended. 
8.  Make a note of the identifier and shared secret as they will be needed to complete the Activate the EQUELLA Resource module steps later. Other options can be enabled as required. 
9. Click Save.
10.  Click Close to close the dialog.

The Shared Secrets plug-in must be enabled (checked). If not already, enable the plug-in:
1.  Check the Enabled checkbox for the Shared Secret plug-in.
2.  Click Yes  to confirm.
3.  Click Exit Console  to close the Administration Console.

NOTE: Only trusted users should be able to see the shared secret, as this information can be used to impersonate any user within EQUELLA.

The next step in the integration process is to download the EQUELLA Moodle Module. 

## Configure Moodle 

This section describes the required configuration changes to Moodle to support the integration. EQUELLA provides a module that allows Moodle users to easily contribute, search and select EQUELLA items, and link them to a course. 

### Download and install the EQUELLA Moodle Modules
The Moodle Modules are available from the Downloads page in the EQUELLA Github repository

To download the Moodle Modules
1.  Navigate to the [Downloads Page](../IntegrationsDownloads.md) in the Equella Github Repository

The EQUELLA Moodle components are made up of three zip files. Each zip contains files relevant to specific sections of the Moodle site. 

Inside the Module to add EQUELLA content as resources or activities zip are the files for the standard module functionality to integrate Moodle with EQUELLA (referred to in this guide as the EQUELLA Resource module).

Inside the Block for users to search EQUELLA directly and Block for users to view their EQUELLA tasks and notifications zips are the files to add portlets to the Moodle front and course pages, allowing direct EQUELLA access (EQUELLA Blocks). 

For complete installation the contents of each zip file need to be extracted to the corresponding folder in the Moodle filesystem.

### Install the EQUELLA Resource Module
1.  To install the EQUELLA Resource module, download the relevant module version of Module to add EQUELLA content as resources or activities and unzip into a newly created path-to-moodle/mod/equella directory.

(NOTE: If installing the Moodle Module on UNIX, ensure the ownership and file permissions match those of the /var/www/moodledirectory/directory.)

### Install the EQUELLA Blocks
1.  To install the EQUELLA Blocks, download the two blocks zips (Block for users to search EQUELLA directly and Block for users to view their EQUELLA tasks and notifications) and unzip them into a newly created path-to-moodle/blocks/equella_search and path-to-moodle/blocks/equella_tasks directories respectively.

### Activate the EQUELLA Resource module
To access Moodle
1.  Open a browser and enter your Moodle URL (e.g. ‘<http://moodle.myequellainstitution.edu>’).
2.  Log in to Moodle as an administrative user.
3.  Select Site administration from the Settings menu. Then click Notifications
4.  Look over the Plugins list. Note the presence of the EQUELLA modules.
5.  Click Upgrade Moodle database now. The initializing of the EQUELLA module will commence.
6.  When completed, you will see confirmation of successful initialization of the EQUELLA module.  The following items will be listed: mod_equella, block_equella_searchc, block_equella_tasks, repository_equella.
7.  Click Continue to move onto the EQUELLA resource configuration page.
8.  Enter the details of your EQUELLA server into the configuration pane. 

a.  Enter the complete EQUELLA URL to your institution with ‘/signon.do’ appended to the URL (e.g. ‘<http://equella.myinstitution.edu/logon.do>’ would become ‘<http://equella.myinstitution.edu/signon.do>’).

b.  Enter the EQUELLA Action (e.g. structured). The ‘structured’ action activates the latest EQUELLA Integration page where users can search the EQUELLA Digital Repository for existing content, contribute new items and select EQUELLA content to link to a course. 

c.  Select a Restrict selections option from the following:
* No restrictions—to not restrict the types of resources course editors can select.
* Items only—to restrict to only items as the type of resources that course editors can select.
* Attachments only—to restrict to only attachments as the type of resources that course editors can select.
* Packages only – this restriction will still allow attachments that aren’t IMS packages to be selected, but they will always display using the IMS package player.

d.  Enter the EQUELLA Options (optional). This string is used to specifically override some built-in actions to restrict the search and contribution options available in the Selection EQUELLA Home page. Available options include:
* powerSearchIds=”UUID” (this option restricts advanced searching to just these advanced searches),
* contributionCollectionIds=”UUID” (this option restricts contribution to just these collections),
where “UUID” is the Universally Unique Identifier of the given entity.

e.  Enter an EQUELLA administrator username. This must be the username of an existing administrator user in EQUELLA who has the VIEW_ITEM privilege granted. This is required for EQUELLA to perform high-level, background functions that don’t have a user session. 

f.  If required, change Default window width and Default window height.

g.  Select Enable LTI and in the Client ID field, enter the Consumer ID for the LTI consumer (e.g. moodleint) and in the Client Secret field, enter the Consumer secret (e.g. 44a1bd760-8371-4155-9bc6-ae632b907a06) created in the Register an LTI consumer steps. NOTE: When LTI is enabled, Shared secrets are disabled for EQUELLA selection sessions. LTI must be enabled to store QTI quiz scores in the Moodle gradebook when QTI 2.1 quizzes linked to courses from EQUELLA are launched. If this functionality is not required, LTI doesn’t have to be enabled, and shared secrets can still be used.

Shared secrets (Default Role settings at minimum) are stored regardless, as they are still used for the Moodle blocks and Drag and Drop functions.

h.  Enter EQUELLA Shared Secret details. These must exist in EQUELLA. In this case they are the same as previously configured. Shared secrets can be configured for different types of users, including: 
* Default role—used for general (read) usage. Typically assigned to students.

  a. Enter EQUELLA Shared Secret ID (e.g. moodle).
  
  b. Enter EQUELLA Shared Secret (e.g. mS3cr3t).

* Each write role in your Moodle site. In this case Teacher role (typically assigned to course contributors) or Manager role (typically assigned to administrators).

   a.  Enter EQUELLA Shared Secret ID.

   b.  Enter EQUELLA Shared Secret.
   
9. Click Save Changes to save the configuration details and complete the EQUELLA Moodle Module setup.

### Test the module installation
To access Moodle
1.  Open a browser and enter your Moodle URL (e.g. ‘<http://moodle.myequellainstitution.edu>’).
2.  Log in to Moodle as an administrator user.
3.  Select a course (e.g. EQ101 – EQUELLA 101) from the My Courses pane to display the Course Weekly outline page. 
4.  Click Turn editing on to display the Add an activity or a resource link. The Add an activity or resource dialog displays. 
5.  Select EQUELLA Resource then click Add to display the EQUELLA Integration page. 

### Activate the EQUELLA blocks
There are two blocks to add as part of the EQUELLA integration. The first is a search block that will allow users to search the EQUELLA repository from inside Moodle and view the results. The other provides users with a summary of their EQUELLA task list from inside Moodle. Access to the tasks in EQUELLA can be made by simply clicking the relevant link.

To access Moodle
1.  Open a browser and enter your Moodle URL (e.g. ‘<http://moodle.myequellainstitution.edu>’).
2.  Log in to Moodle as an administrator user.
3.  Select a course (e.g. Science - Physiology) from the My Courses pane to display the course Weekly outline page. 
4.  Click Turn editing on to display the Add a block drop-down list
5.  Select the EQUELLA block options one at a time. 
6.  Upon selecting an option, Moodle will recognize the selection and refresh the page, updating the layout.

Note that the EQUELLA Tasks block can also be added on the Moodle front page.

### Test the blocks installation
To access Moodle
1.  Open a browser and enter your Moodle URL (e.g. ‘<http://moodle.myequellainstitution.edu>’).
2.  Log in to Moodle as an administrator user.
3.  Select a course (e.g. Science - Physiology) from the My Courses pane to display the course Weekly outline page. 
4.  In the EQUELLA Search block, click the Search EQUELLA link.
5.  Enter a search term into the search box and click Search.
6.  All results matching the search query will be returned from the EQUELLA repository.
7.  Click the View link alongside a resource to open it.

### Activate the EQUELLA repository 

Activate the EQUELLA repository plug-in to enable searching of the EQUELLA repository to find and retrieve files from when using a file picker from inside Moodle. 

1.  Open a browser and enter your Moodle URL (e.g. ‘<http://moodle.myequellainstitution.edu>’).
2.  Log in to Moodle as an administrator user.
3.  From the Moodle home page expand the Site administration menu folder. 
4.  Expand the Plugins menu folder, and then the Repositories menu folder
5.  Click the Manage repositories link to open the configuration pane.
6.  Find the EQUELLA repository drop-down menu, and expand it to reveal the options.
7.  Select Enabled and visible to make the EQUELLA repository a selectable option in a file picker. The Configuration for EQUELLA repository page displays. 
8.  Click Save. 
9.  Scroll down to EQUELLA Repository once again, and select the Settings link. The Configuration for EQUELLA repository page displays.
10.  Click Create a Repository Instance. The Create a repository instance page displays. 
11.  Enter a Name for the EQUELLA repository (e.g. EQUELLA). This name displays in the file picker. If multiple EQUELLA repositories are to be configured, using a descriptive name is useful (e.g. University of Tas, RMIT etc.).
12.  Enter the complete EQUELLA URL for the relevant institution with ‘/signon.do’ appended to the URL (e.g. ‘<http://equella.myinstitution.edu/logon.do>’ would become ‘<http://equella.myinstitution.edu/signon.do>’).
13.  Enter the EQUELLA Options (optional). This string is used to specifically override some built-in actions to restrict the search and contribution options available on the EQUELLA Integration page. 
14.  Enter the Default role settings, Shared secret ID and Shared secret that have been set in the EQUELLA instance. 
15.  Enter the Shared secret IDs and Shared secrets for Manager role settings, Teacher role settings and/or EQUELLA Web Service Role settings if relevant.
16.  Click Save. The repository instance displays on the EQUELLA repository page.

### Test the Repository installation
To access Moodle
1.  Open a browser and enter your Moodle URL (e.g. ‘<http://moodle.myequellainstitution.edu>’).
2.  Log in to Moodle as an administrator user.
3.  Select a course (e.g. DOC1 - Documentation) from the My Courses pane to display the course Weekly outline page. 
4.  Click Turn editing on to enable the editing options. 
5.  With a resource already present in your course, select the Edit link, then Edit settings from the menu. 
6.  On the Updating EQUELLA Resource page, click the Insert/Edit image button in the editor.  The image properties dialog displays. 
7. Click Browse repositories to open the File picker window.
8.  EQUELLA (or the name entered for the repository instance) displays in the left-hand menu. Click the EQUELLA link to search the repository. 

## Enable Moodle drag and drop auto add to EQUELLA function  

Files can be automatically contributed to EQUELLA when dragging and dropping onto a Moodle course page, or onto the Content, Select files panel from the Adding a new File page in Moodle. The system first checks to see if the file already exists in EQUELLA. If so, it creates a link to the file, otherwise it contributes the file into the collection allocated for the ‘Quick contribute’ function.

In versions prior to EQUELLA 6.2, the drag and drop/auto add function used an OAuth client, but in order to pass through the correct user details to EQUELLA, all subsequent releases use a Shared secret, which is already set up when the integration is configured.

### Configure Moodle for drag and drop/auto add to EQUELLA
To configure Moodle for drag and drop/auto add to EQUELLA 
1.  Log in to Moodle as an administrator.
2.  From the Moodle home page expand the Site administration menu folder, then select Plugins, Activity modules, EQUELLA Resource. 3.  Scroll to the bottom of the page, where the Shared Secret Settings section is visible. 
3.  Make sure there is a Shared secret ID and Shared secret for Default role settings. This would have been configured during the initial integration configuration process.
4.  Select the required Intercept drag and drop files option:
* Don’t intercept files – always adds files as file resources locally in Moodle.
* Display file destination dialog – displays a confirmation dialog asking the user to select where the file should be saved. 
* Options are:
    * Contribute to EQUELLA – automatically contributes the file to EQUELLA, with the file name as the Title and Description, and adds a link to that EQUELLA record in Moodle.
    * Add image to course page - shows the full sized image on the course page instead of a link. This option only displays for image files.
    * Create file resource – saves the file locally in Moodle as a file resource.
6.  Click Save Changes.

## QTI 2.1 with Moodle EQUELLA integrations  

QTI 2.1 quizzes can be linked to Moodle courses from EQUELLA, then launched and submitted. Quiz answers are stored in the EQUELLA database, and a score is calculated on submitting the quiz. The score is passed back to the Moodle gradebook, and can be viewed by users with the appropriate permissions.

### Configuring an EQUELLA/Moodle integration for QTI 2.1 gradebook scoring

EQUELLA enables QTI quizzes to be linked to Moodle courses and launched and submitted from those courses. To enable the score to be stored in the Moodle gradebook, an LTI consumer must be configured.

To configure the LTI consumer
1.  Create an LTI consumer record in EQUELLA. 
2.  Map the LTI roles. 
3.  Log in to Moodle as an administrator.
4.  From the Moodle home page expand the Site administration menu folder, then select Plugins, Activity modules, EQUELLA Resource.
5.  Scroll to the LTI Settings section. 
6.  Select Enable LTI and enter the Client (Consumer) ID (e.g. moodleint) and Client (Consumer) Secret (e.g. 44a1bcd0-dea5-4976-90c3-80b1cd421144) created in the prior Register an LTI consumer steps.
NOTE: Once LTI has been enabled, Shared secrets are disabled for EQUELLA selection sessions. The Default role settings Shared secret is still used for the Moodle drag and drop/auto add to EQUELLA and Moodle blocks functions.
7.  Click Save Changes.
QTI 2.1 quizzes launched from Moodle courses will now automatically store the score in the user’s Moodle gradebook.

## Troubleshoot an unsuccessful integration

If the integration is unsuccessful, these are the points to check first:
1.  Check that both the Moodle server and the EQUELLA server have the same UTC time.
2.  Ensure the Shared Secret plug-in in the EQUELLA User Management tool is enabled.
3.  Check the EQUELLA Moodle Module file is installed.
4.  Check the configuration data in Moodle. 

## Upgrade the EQUELLA Moodle Module
To upgrade the EQUELLA Moodle Module
1. Remove the existing equella folder in the path-to-moodle\mod directory and replace it with the latest version of the equella folder.

## Viewing the EQUELLA Moodle Module change log
The EQUELLA Moodle Module change log enables administrators to view bug fixes and new features added to the current EQUELLA module release.

To view the EQUELLA Moodle Module change log
1.  Log in to Moodle as an administrative user.
2.  Select Site administration from the Administration menu. 
3.  Select Plugins, Activity modules then EQUELLA Resource. 
4.  Click the View change log link at the top of the page to open the change log in a new browser tab and view the Moodle Module information.4. 4. 