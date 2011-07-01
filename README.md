What is it?
===========
At Billups Design we use a modified version of Paul Irish's HTML5 Boilerplate to serve as a "kickstarter" of sorts for our frontend development. We've taken Paul Irish's HTML5 boilerplate code and adapted it to a set of starter files for our ExpressionEngine2 projects.

Its meant to help get an EE2 project off the ground in a hurry by supplying a set of html templates, CSS, JS, and commonly used php scripts.


Installation
------------
Starting with a fresh install of ExpressionEngine2

1. Upload the `assets` folder, 'templates' folder, and 'robots.txt' file to the root directory of your server.
2. Upload '/htaccess.txt` file to the root directory of your server and rename to `.htaccess` with no .txt extension.
3. Login to your EE dashboard and go to Design>Templates>Global Preferences
4. Change Allow Templates to be Saved as Files to "Yes"
5. Change the "Basepath to Template File Directory" to point to the 'templates' folder in your root.
6. Go to the Template Manager and edit the home group.
7. Check the box that says "Make the index template in this group your site's home page?"
8. Go to the Template Preferences Manager and select code-header and code-footer in the site group.
7. For both templates, select 'Yes' on Allow PHP and 'Output' on PHP Parsing Stage and Update.


What's Included
===============

site.group
----------
Inside of the "site" template group there are 5 files. They are all global files that don't pertain to a particular section of the website.

*404.html*
This file is a generic 404 page that you can redirect to for various EE 404s.

*code_footer.html*
This file has all of the JS that you include just before the closing `</body>` tag. In addition to the `</body></html>` tags.

*code_header.html*
This file is a html header that begins with `<!DOCTYPE html>` and ends at the opening `<body>` tag. It includes all of the various CSS,JS, conditional comments etc. It is well commented to explain the purpose of all the various components.
	
*footer*
This file is meant to hold traditional web page footer markup. Such as copyright, footer navigation, etc.

*header*
This file is meant to hold a traditional web page header. Such as the logo and main navigation.

home.group
----------
This folder is meant to house the default index of the website. Configured in the Installation steps above.

ie6.group
---------
This folder is meant to house the page ie6 users are redirected to and prompted to upgrade their browser. This is optional (see usage instructions below) and something we personally choose to use at Billups Design.

Usage
=====

Default Template Configuration
------------------------------
Each web page should have the following template structure in this order

`{site/code-header}
{site/header}
{group/template}
{site/footer}
{site/code-footer}`


Every new page template should have the following structure

`{embed="site/code-header" title="Page title" description="Meta description" keywords="Meta keywords"}
{embed="site/header"}
	Markup goes here
{embed="site/footer"}
{embed="site/code-footer"}`

Using the title attribute is helpful for changing the `<title>` tag with the following code snippet _(which is already in place in the site/code\_header.html template)._
`{if embed:title}{embed:title}{/if}`
Using the description attribute is helpful for changing the `<meta name="description">` tag with the following code snippet _(which is already in place in the site/code\-header.html template)._
`{if embed:description}<meta name="description" content="{embed:description}" />{/if}`
Using the keywords attribute is helpful for changing the `<meta name="keywords">` tag with the following code snippet _(which is already in place in the site/code\-header.html template)._
`{if embed:keywords}<meta name="keywords" content="{embed:keywords}" />{/if}`

Using the Assets Folder
-----------------------
Rather than put js and css files in EE template groups and use the images folder at the root we've constructed a folder called "assets" that lives in the root of the site. This file contains all external files used to support your EE template files. 

IE6 support configuration
-------------------------
By default EE Kickstarter redirects users with IE6 to an "Upgrade Your Browser" page. If you wish to disable this.

1. Remove Lines 13-21 in the site/code\-header.html file
2. Remove the ie6.group folder in `/system/expressionengine/templates/default_site`
3. Remove the ie6 folder in `/assets/`

Removing index.php from URLs
----------------------------
We've already included a great `.htaccess` file from the HTML5 Boilerplate, but we've modified the last couple lines to use the "Exclude Method" of removing index.php from EE urls. You can add more files and directories to be excluded from URL rewriting by modifying line 175 of htaccess.txt where it reads...
`RewriteCond $1 !^(assets|images|system|themes|favicon\.ico|robots\.txt|index\.php) [NC]` 

You must also do the following to fully remove index.php from URLs generated by EE template code.

1. Login to EE dashboard
2. Go to Admin > General Configuration
3. Change "Name of your site's index page" to be blank.