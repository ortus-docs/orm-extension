---
description: Get up and running in seconds!
---

# Installation

## CommandBox

### Via `lucee-extensions` system property

You can install this extension at server start time by passing the extension ID into the `lucee-extensions` environment variable:

```bash
box server start cfengine=lucee@5.4 -Dlucee-extensions='D062D72F-F8A2-46F0-8CBC91325B2F067B'
```

To install a specific version, set that by appending `;version=1.2.3` to the extension ID:

```bash
box server start cfengine=lucee@5.4 -Dlucee-extensions='D062D72F-F8A2-46F0-8CBC91325B2F067B;version=6.4.0'
```

(For all available version numbers, see our [Release History](release-history.md) or the [GitHub Releases page](https://github.com/Ortus-Solutions/extension-hibernate/releases).)

### Via `lucee-extensions` environment variable

We recommend setting the `lucee-extensions` environment variable in your `server.json` file. This ensures that anyone can run `server start` from CommandBox to install all the necessary Lucee extensions:

{% code title="server.json" %}
```json
{
    "app":{
        "cfengine":"lucee@5"
    },
    "env":{
        "lucee-extensions":"D062D72F-F8A2-46F0-8CBC91325B2F067B;version=6.4.0"
    }
}
```
{% endcode %}

This config instructs Lucee (not CommandBox) to install the Ortus ORM Extension when Lucee starts up.

### Via Box Install

Use `box install` if you wish to install the extension into an already installed Lucee server:

```bash
box install D062D72F-F8A2-46F0-8CBC91325B2F067B@6.4.0
```

_This method will not work until the Lucee server has been installed._

## From the Lucee Server Admin

You can manually install the extension by opening the Lucee server admin page and browsing to `Extension > Applications` page, where you'll see a "Ortus ORM Extension" option. Clicking this option will open the installation screen, where you can choose any extension version and click "Install" to install from Forgebox.

### Direct Download

You can also download a `.lex` file from [our downloads page](https://downloads.ortussolutions.com/#/ortussolutions/lucee-extensions/ortus-orm/) and upload this through the Lucee Server admin's Applications page.
