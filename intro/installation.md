---
description: Get up and running in seconds!
---

# Installation

## CommandBox

You can install this extension by adding the extension ID to the `lucee-extensions` environment variable and restarting the server:

<pre class="language-bash"><code class="lang-bash"><strong>box server set env.LUCEE_EXTENSIONS="D062D72F-F8A2-46F0-8CBC91325B2F067B" &#x26;&#x26; box restart
</strong></code></pre>

You can install a specific version by appending a version string to the extension ID:

```bash
box server set env.LUCEE_EXTENSIONS="D062D72F-F8A2-46F0-8CBC91325B2F067B;version=6.5.2" && box restart
```

(For all available version numbers, see our [Release History](release-history.md) or the [GitHub Releases page](https://github.com/Ortus-Solutions/extension-hibernate/releases).)

Running the `box server set env.lucee-extensions` command will edit your `server.json` file to look something like this:

{% code title="server.json" %}
```json
{
    // ...
    "env":{
        "LUCEE_EXTENSIONS":"D062D72F-F8A2-46F0-8CBC91325B2F067B;version=6.5.2"
    }
}
```
{% endcode %}

This config instructs Lucee (not CommandBox) to install the Ortus ORM Extension when Lucee starts up.

## From the Lucee Server Admin

You can manually install the extension by opening the Lucee server admin page and browsing to `Extension > Applications` page, where you'll see a "Ortus ORM Extension" option. Clicking this option will open the installation screen, where you can choose any extension version and click "Install" to install from Forgebox.

### Direct Download

You can also download a `.lex` file from [our downloads page](https://downloads.ortussolutions.com/#/ortussolutions/lucee-extensions/ortus-orm/) and upload this through the Lucee Server admin's Applications page.
