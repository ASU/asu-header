# ASU Global Header & Footer


The ASU web standards established a single standard header, which replaces all previous headers. Consequently, headers with endorsed logos (custom headers) are no longer supported. The single standardized header is the only option.

Header versions used in the below instructions may change as official releases are completed.

**Latest build is 4.7**

## 


## Adding to a non-Drupal site

If you're using the header and footer on a non-Drupal site, follow the instructions for your application language below.

### HTML (APACHE WITH SSI SUPPORT)
*Note*: You must have the path /afs/asu.edu/www/asuthemes mounted in Apache as /asuthemes in your document root. For this, the server must be able to access AFS. Sites already in AFS (e.g., www.asu.edu/my-site) and accounts on the legacy ASU Web Hosting Service (i.e., DirectAdmin) already have this access.

**Header: Place above `</head>` tag:** `<!--#include virtual="/asuthemes/4.7/heads/default.shtml"-->`

**Google Tag Manager: Place below `<body>` tag:** `<!--#include virtual="/asuthemes/4.7/includes/gtm.shtml"-->`

**Header: Place below Google Tag Manager:** `<!--#include virtual="/asuthemes/4.7/headers/default.shtml"-->`

**Footer: Above `</body>` tag:** `<!--#include virtual="/asuthemes/4.7/includes/footer.shtml"-->`

### PHP

**Header: Place above `</head>` tag:** `<?php echo file_get_contents('http://www.asu.edu/asuthemes/4.7/heads/default.shtml'); ?>`

**Google Tag Manager: Place below `<body>` tag:** `<?php echo file_get_contents('http://www.asu.edu/asuthemes/4.7/includes/gtm.shtml'); ?>`

**Header: Place below Google Tag Manager:** `<?php echo file_get_contents('http://www.asu.edu/asuthemes/4.7/headers/default.shtml'); ?>`

**Footer: Above `</body>` tag:** `<?php echo file_get_contents('http://www.asu.edu/asuthemes/4.7/includes/footer.shtml'); ?>`

## Adding to a Drupal Site

### Webspark

If you are building a new site, the ASU Webspark Site Builder is the preferred and recommended way to build an ASU web standards compliant site. In Webspark, the ASU header and footer are enabled and work out-of-the-box.

### Drupal (stand-alone)

If you must build in Drupal 7, the [ASU Brand Module](https://drupal.asu.edu/resources/docs/modules/asu-brand-module) adds the ASU header and footer to any Drupal site. (Thanks to Marcus Anthony for creating the original version of this module and making it available to the community.)

There is no Drupal 6 specific method for adding this version of the ASU header and footer. The method described in the "PHP" section above should work for Drupal 6.

### To a non-responsive site

Newer versions of the Web Standard Header & Footer include a file called `legacy.shtml` in the `heads` directory.
Simply include that file instead of `default.shtml` as in the following example of the PHP implementation.

**Header: Place above `</head>` tag:** `<?php echo file_get_contents('http://www.asu.edu/asuthemes/4.7/heads/legacy.shtml'); ?>`

**Google Tag Manager: Place below `<body>` tag:** `<?php echo file_get_contents('http://www.asu.edu/asuthemes/4.7/includes/gtm.shtml'); ?>`

**Header: Place below Google Tag Manager:** `<?php echo file_get_contents('http://www.asu.edu/asuthemes/4.7/headers/default.shtml'); ?>`

**Footer: Above `</body>` tag:** `<?php echo file_get_contents('http://www.asu.edu/asuthemes/4.7/includes/footer.shtml'); ?>`

## Configuring the header

The header search behavior and site title are configurable. Links can be added to the header mobile menu as well. See how to configure the header for Drupal and non-Drupal sites.

### On a non-Drupal site

On non-Drupal sites, the configuration changes must be made manually by assigning values to pre-defined JavaScript variables.

#### Search Collection

The search by default searches against the ASU Google Search Appliance. To add a search collection—a search of just your site—you will need to add this variable in your javascript file and set it to your collection.

```javascript
ASUHeader.gsa = 'Collection'
```

If you need assistance in finding your collection or creating a new collection, create a support ticket.

#### Mobile menu

In addition to the ASU global navigation menu, the ASU header can consume a site's local navigation menu and render it as part of its mobile menu. The mobile menu is visible when the browser viewport size is less than 991px.

The ASU header uses JavaScript to append the local navigation menu items to the mobile menu. The site menu needs to provided as a JSON formatted object:

```
ASUHeader.site_menu = 
{
    json: '[{  
             "title":"Home",
             "path":"http://www.asu.edu/absolute_path"
          },
          {  
             "title":"Degree Programs",
             "path":"/absolute_path/page",
             "children":[  
              {  
                 "title":"Admissions",
                 "path":"/?url=variable",
                 "children":[  
                    {  
                       "title":"Student Life",
                       "path":"/#hash"             
                    }
                 ]
              },
              {  
                 "title":"Ross",
                 "path":"https://www.asu.edu/"
  }
              }
             ]
          },
          {  
             "title":"Test",
             "path":"http://www.asu.edu/",
             "children":[  
              {  
                 "title":"Beast Layout",
                 "path":"http://www.asu.edu/"
              },
              {  
                 "title":"Landing Page Test",
                 "path":"http://www.asu.edu/"
              },
              {  
                 "title":"Moscone w\/ 100% Banner Title",
                 "path":"https://www.asu.edu/"
              },
              {  
                 "title":"Plain Moscone Layout",
                 "path":"http://www.asu.edu/layout/this/that/theother"
              }
             ]
          }]'
};
```

#### Site title & Parent Organization

The WSHF can generate a Desktop site title, as well as provide a parent organization to be printed under the ASU Logo at the top of the page. These will also translate to the mobile menu.

Ex.

```javascript
ASUHeader.site_title = {title: "Name of Site", parent_org: "Name of Parent Organization", site_url: "URL of for title link", parent_org_url: "URL of for parent org title link"};
```

_\*Obsolete\*_ The site title can be added specifically to the mobile menu system with the following.

```javascript
ASUHeader.site_menu.site_name = 'Name of site';
```

### On a Drupal site

On Drupal sites, the header is created by the ASU Brand Module and configuration changes are made through the administration interface directly on the site.

#### Search

The search by default searches against the ASU Google Search Appliance. To add a search collection—a search of a specific web site or collection of web sites—to a stand-alone Drupal site, you should install the ASU GSA Search Module. On Webspark sites, this module is already installed for you.

Follow the instructions for configuring the ASU GSA Search Module.

If you need assistance in finding your collection or creating a new collection, create a support ticket.

#### Mobile menu

For Drupal 7 and Webspark sites, the ASU Brand Module (version 7.x-1.7 and above) generates the site menu object by default. Modify menu headers and items by going to the Admin > Structure > Menus > Main Menu page ( /admin/structure/menu/manage/main-menu ). Create menu items for your pages on each pages' edit form.

There is a configuration option in the ASU Brand Module (version 7.x-1.7 and above) to specify a different menu for the Mobile menu.

#### Site title

For Drupal 7 and Webspark sites, change the site title on the Admin > Configuration > System > Site information page ( admin/config/system/site-information ).

