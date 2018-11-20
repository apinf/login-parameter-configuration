# login-parameter-configuration
Describes management of login platforms' parameters

Managing OAuth login parameters in APInf
========================================

Different OAuth logins
----------------------

In some cases an OAuth login possibility is needed in addition to the basic login with password and username.

Currently in APInf platform there are three OAuth login possibilities:
- github
- fiware
- HSL

The github and fiware OAuth logins are included in as Meteor packages, 
however the HSL OAuth login program code is a part of APInf codebase.
All the OAuth login functionalities rely on Meteor account related packages.


Starting to use OAuth login
---------------------------

Each of those OAuth logins needs certain parameters to be set in order to be able to connect the OAuth servers in question.

The flow is as follows:

If the OAuth login service is not configured, in Sign_in page the User is prompted to provide configuration parameters.

The configuration parameters given via prompt are stored into a MongoDB collection ie. the external database:

      meteor_accounts_loginServiceConfiguration

If the OAuth login service is configured, the configuration parameters are read from database and 
a request is sent to OAuth server in order to get the credentials.


Modifying OAuth login configuration parameters
----------------------------------------------

Once stored in meteor_accounts_loginServiceConfiguration collection, there is no UI provided to update 
the configuration parameters. 
Thus in APInf there is implemented an internal interface for configuration parameter update.

For updating the configuration parameters there is used another MongoDB collection, ie. the internal database:

     LoginPlatforms

A signed in Admin User can choose selection Login Platforms to open a page for configuration parameter update.


Update of configuration parameters
----------------------------------

From meteor_accounts_loginServiceConfiguration to LoginPlatforms

Every time when the login platforms page is opened, the configuration parameter values in collection LoginPlatforms 
are updated to be same as in collection meteor_accounts_loginServiceConfiguration.

From LoginPlatforms to meteor_accounts_loginServiceConfiguration

When parameter values are modified and saved in Login platforms page, the new values are stored into both collections:
LoginPlatforms and meteor_accounts_loginServiceConfiguration. 


Removing configuration parameters
---------------------------------

It is also possible to remove configuration parameter values.

When Admin User empties the parameter values in login platforms page and saves it, the values are
removed from both collections.

Note! When configuration parameters are removed from a OAuth service, they can be added either by using Sign_in page
or Login Platforms page.


Adding configuration parameters
-------------------------------

Admin User can add configuration parameter values using Login platforms page. 

When added values are saved, they are stored in both databases.






