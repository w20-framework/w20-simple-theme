---
title: "Overview"
theme: "Simple theme"
repo: "https://github.com/seedstack/w20-simple-theme"
author: "SeedStack"
description: "W20 theme providing a basic top-bar including a navigation menu and standard application controls."
min-version: "15.7+"
menu:
    SimpleTheme:
        weight: 10
---

There are two ways of adding this theme to your application, depending how your W20 frontend is handled.

# Separate frontend

In the case of a separate frontend (not served from resource JARs), you need to add the `w20-simple-theme` to your 
`bower.json` file. Check for the latest release [here](https://github.com/seedstack/w20-simple-theme/releases).

# JAR-served frontend

If the frontend files are served from resource JARs, the W20-bridge add-on packages this theme under the following artifact:
 
    <dependency>
        <groupId>org.seedstack.addons</groupId>
        <artifactId>w20-bridge-web-simple-theme</artifactId>
    </dependency>

Simply add it to the Web module of your project.