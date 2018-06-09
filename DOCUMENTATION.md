## Requirements
*Requirement:* Statamic v2.6.x

## Installation
1. Rename the folder `GoogleAnalytics` and copy it to your `site/addons` folder
2. Run `php please update:addons` to install the depencency.

## Tracking Configuration
Use the settings to configure your tracking id and other Google Analytics settings or create a settings file in `site/settings/addons/google_analytics.yaml`
```
tracking_id: UA-*******-*
async: false
beacon: false
display_features: false
link_id: false
track_uid: false
ignore_admins: false
debug: false
trace_debugging: false
disable_sending: false

```

## Tracking Tag
Add the Google Analytics tag to your theme layout file just before your close `</head>` tag.

```
  {{ google_analytics }}
```

## Environment Support
Use Statamic's built in [environment specific settings](https://docs.statamic.com/settings#environment) to specify different settings for Google Analytics in development or testing.

## Reporting Setup
To use the reporting features of the Google Analytics Addon you will have to create an account with Google, sign in and set it up with credentials to use Google's APIs.

### Create A Project & Credentials
1. Go to [Google API’s site](https://console.developers.google.com/apis) and select `Select a project`, and make a new project, or make sure the correct project is selected from the header.

2. Enable the Google Analytics API by navagiating to `Libary` in the left hand side navagation. Search for `Google Analytics API`, slect this Libary to view the description and enable it. (Don't confuses this with the `Google Analytics Reporting API`)

3. Create Credentials by clicking on the `Create Credentials` button in the notification (on the top right) or by going to the `Credentials` item in the left hand side navagation.

4. Select `Google Analytics API` from the dropdown for what API are you using?

5. Select `Web Server ...` for where will you be calling the API from.

6. Select `Application Data ...` for what data will you be accessing.

7. Select `No, I'm not using them` for Are you using Google App Engine or Google Compute Engine? (unless you are)

8. Click the button `What credentials do I neeed?`

9. Enter a service account name (`statamic` for example)

10. Select `Service Account > Service Account User` for the role

11. Select `JSON` as the Key type

12. Click `continue`, save the key file to a safe location, we will be using it later (and keep it private).

### Granting Permission to your Google Analytics Property
1. Go to the [Google Analytics Website](https://analytics.google.com/analytics) and navagate to the settings for the appropiate property.

2. Select `User Managment` under the view column.

3. Add a new user with `Read & Analize` access using the `client_email` value from the JSON file you downloaded.

4. Get the `View ID` by clicking on `View Settings` on the Google Analytics website.

### Setting it all up
1. Add the `View ID` to the Google Analytics Settings under the `Reporting Configuration` section in the Statamic Control panel.

2. Upload the JSON file & rename it to `site/settings/addons/google-analytics-credentials.json` or some other location outside of your version control system. Just make sure to set the path in the configuration (including the file name) if you put the file in a diffrent location.

## Widgets
There are a number of widgets you can add to the Statamic Dashboard to quickly view reports, in addtion to the Google Analytics report pages in the navagation.

Tye pipe `|` below indicates options, only one of the options should be used.

### Visitiors & Page Views
```
-
  type: GoogleAnalytics
  width: half | full
  dates: show | hide
```

### MostVisited
```
-
  type: GoogleAnalytics.MostVisited
  width: half | full
  dates: show | hide
```

### Browsers
```
-
  type: GoogleAnalytics.Browsers
  width: half | full
  type: doughnut | bar | horizontal-bar
  dates: show | hide
```

### Referals
```
-
  type: GoogleAnalytics.Referals
  width: half | full
  type: doughnut | bar | horizontal-bar
  dates: show | hide
```

## Access Restrictions
By default anybody with *CP Access* will be able to see Google Analytics reports.

If you want to restrict what users can see the Google Analytics reports you can the slugs of the roles you wish to grant access to on the settins page under `Roles with Access`.

Example:
```
roles_with_access:
  - admin
  - blog-editor
  - editor
```

## Add Blockers
- uBlock Origin, and possibly other addons of this type can cause the scripts this addon use to not load. If you disable the plugin for your domain the scripts should load, and the addon should work.
