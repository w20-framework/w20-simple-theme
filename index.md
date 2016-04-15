---
title: "Basics"
name: "Simple theme"
repo: "https://github.com/seedstack/w20-simple-theme"
author: "Adrien LAUER"
description: "W20 theme providing a basic top-bar including a navigation menu and standard application controls."
min-version: "16.4+"
weight: -1
image: screenshot-01.png
date: 2015-07-27
zones:
    - Themes
menu:
    SimpleTheme:
        weight: 10
---

There are two ways of adding this theme to your application, depending how your W20 frontend is handled.

# Standalone frontend

In the case of a standalone frontend, you need to add the `w20-simple-theme` to your `bower.json` file. Check for the latest release [here](https://github.com/seedstack/w20-simple-theme/releases).

# JAR-served frontend

If the frontend files are served from resource JARs, the W20-bridge add-on packages this theme in the following artifact:
 
{{< dependency g="org.seedstack.addons.w20" a="w20-bridge-web-simple-theme" >}}

Simply add it to your project `pom.xml`.

# Configuration

## Fragment declaration

To include the theme, declare it in your W20 application configuration file (If you are using the bridge addon it will be included by default).

```
"bower_components/w20-simple-theme/w20-simple-theme.w20.json": {
    "modules": {
        "main": {}
    }
}
```

## Options

* `categories`: (Array of strings)  Ordered array of displayed menu categories
* `hideViews`: (Boolean) Hide the views section
* `hideConnectivity`: (Boolean) Hide the connectivity indicator
* `hideCulture`: (Boolean) Hide the culture chooser
* `hideSecurity`: (Boolean) Hide the security status
* `routes`: (Array of strings) Routes to show directly in the topbar
* `logo`: (Object) Options for the topbar logo
    * `ìmage`: (String) url of the logo image
    * `url`: (String) url of the logo link
    * `target`: (String) target of the logo link (defaults to _self)
    * `tooltip`: (String) text of the logo tooltip (defaults to the `url` attribute)

## Menu routes

Routes declaration of fragments are aggregated in the sidebar menu. You can group related route under a category by declaring a `category` attribute on the route declaration.

```
"routes": {
    "topLevelRoute": {
        "templateUrl":"{Fragment}/views/topLevelRoute.html",
        "controller":"TopLevelRouteController as tlr",
    },
    "route1OfCatOne": {
        "templateUrl":"{Fragment}/views/route1.html",
        "controller":"Route1Controller as rc1",
        "category": "catOne"
    },
   "route2OfCatOne": {
       "templateUrl":"{Fragment}/views/route2.html",
       "controller":"Route1Controller as rc2",
       "category": "catOne"
   }
}
```

The category will appear as an i18n key in your route (`application.viewcategory.[category name]`) which you can
then localize.

You can order the category in the menu by delcaring a `navigation` property in your fragment manifest:

```
"navigation": {
    "": [ "catTwo", "catOne"]
}
```

## Topbar actions

The topbar will automatically include actions such as a culture dropdown, login/logout button or connectivity status if 
the relevant module have been declared and if these actions have not been hidden using `hideXXXX` properties.

You can include your own actions using the `MenuService`:

* First you need to register an action type:

```
service.registerActionType('my-action-type', {
    templateUrl: '{Fragment}/templates/action-my-action.html',
    showFn: function () {
        var show = true;
        // You can specify conditions for displaying the action
        return show;
    }
});
```

* Then you can add this action to the topbar:

```
service.addAction('action', 'my-action-type', {
    sortKey: 300
});
```

This register an action of name 'action' of type 'my-action-type'. The last parameter is an
object which will extend the default one you provided in the action type registration. Use
the `sortKey` attribute to order your actions display.
