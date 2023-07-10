---
description: Get up and running in seconds!
---

# Installation

## CommandBox

You can install this extension into a _preconfigured_ Lucee server via Commandbox:

```bash
box install D062D72F-F8A2-46F0-8CBC91325B2F067B
```

This will not work unless `box server start` has been run first to set up the Lucee engine directories. Use `--dryRun` to set up the Lucee server without actually starting the server process. This will prevent ORM from attempting to initialize before the extension is installed:

```bash
box> server start --dryRun
box> install D062D72F-F8A2-46F0-8CBC91325B2F067B
box> server start
```

## JVM Argument

You can also use the Lucee JVM argument to install the extension at startup

```json
-Dlucee-extensions=D062D72F-F8A2-46F0-8CBC91325B2F067B
```

## From the Lucee Server Admin

You can manually install the extension by opening the Lucee server admin page and browsing to `Extension > Applications` page, where you'll see a "Ortus ORM Extension" option. Clicking this option will open the installation screen, where you can choose any extension version and click "Install" to install from Forgebox.&#x20;

## Direct Download

You can also download a .lex file from [our downloads page](https://downloads.ortussolutions.com/#/lucee/extensions/hibernate/) and upload this through the main Applications page.
