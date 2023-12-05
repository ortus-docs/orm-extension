---
description: Get up and running in seconds!
---

# Installation

## CommandBox

You can install this extension at server start time by passing the extension ID into the `lucee-extensions` environment variable:

```bash
box server start cfengine=lucee@5.4 -Dlucee-extensions='D062D72F-F8A2-46F0-8CBC91325B2F067B'
```

To install a specific version, set that by appending `;version=1.2.3` to the extension ID:

```bash
box server start cfengine=lucee@5.4 -Dlucee-extensions='D062D72F-F8A2-46F0-8CBC91325B2F067B;version=6.2.0'
```

For all available version numbers, see our [Release History](release-history.md) or the [GitHub Releases page](https://github.com/Ortus-Solutions/extension-hibernate/releases).)

Use `box install` if you wish to install the extension into an already running Lucee server:

```bash
box install D062D72F-F8A2-46F0-8CBC91325B2F067B@6.1.0
```

## From the Lucee Server Admin

You can manually install the extension by opening the Lucee server admin page and browsing to `Extension > Applications` page, where you'll see a "Ortus ORM Extension" option. Clicking this option will open the installation screen, where you can choose any extension version and click "Install" to install from Forgebox.

### Direct Download

You can also download a `.lex` file from [our downloads page](https://downloads.ortussolutions.com/#/ortussolutions/lucee-extensions/ortus-orm/) and upload this through the Lucee Server admin's Applications page.
