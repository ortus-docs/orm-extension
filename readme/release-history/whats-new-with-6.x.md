# What's New With 6.x

### [6.2.0](https://github.com/Ortus-Solutions/extension-hibernate/compare/v6.1.0...v6.2.0) - 2023-08-03

### ♻️ Changed

#### Hibernate Upgraded from 5.4 to 5.6

This brings the Hibernate dependencies up to date (released Feb. 2023), and should not change any CFML-facing features for *most* users. (See [CLOB columns in Postgres81](#clob-columns-in-postgres81))

See the migration guides for more info:

* [Hibernate 5.4 -> 5.4 migration guide](https://github.com/hibernate/hibernate-orm/blob/5.5/migration-guide.adoc)
* [Hibernate 5.5 -> 5.6 migration guide](https://github.com/hibernate/hibernate-orm/blob/5.6/migration-guide.adoc)

#### CLOB columns in Postgres81

Due to the Hibernate 5.6 upgrade, if you are using the `PostgreSQL81` dialect and have `CLOB` columns in your database, [it is recommended you migrate existing text columns for LOBs to `oid`](https://github.com/hibernate/hibernate-orm/blob/5.6/migration-guide.adoc#changes-to-the-ddl-type-for-clob-in-postgresql81dialect-and-its-subclasses).

#### Default EHCache Configuration

The default `ehcache.xml` for EHCache changed to include [`clearOnFlush="true"`](https://www.ehcache.org/apidocs/2.10.1/net/sf/ehcache/config/CacheConfiguration.html#clearOnFlush) and [`diskSpoolBufferSizeMB="30MB"`](https://www.ehcache.org/apidocs/2.10.1/net/sf/ehcache/config/CacheConfiguration.html#diskSpoolBufferSizeMB) properties to match [Adobe ColdFusion 9's  default `ehCache.xml` config](https://helpx.adobe.com/coldfusion/developing-applications/coldfusion-orm/performance-optimization/caching.html). Both these values represent default settings in EHCache itself.

### 🐛 Fixed

* Fixes handling of `"timezone"`-typed column values. Previously, fields defined with `ormtype="timezone"` would neither use the `default` value nor allow new values to be set. [OOE-10](https://ortussolutions.atlassian.net/browse/OOE-10)
* Fixes entity state changes in `preInsert()`/`preUpdate()` listeners for properties with no `default` defined. [OOE-9](https://ortussolutions.atlassian.net/browse/OOE-9)

### [6.1.0](https://github.com/Ortus-Solutions/extension-hibernate/compare/v6.0.0...v6.1.0) - 2023-07-14

#### ♻️ Changed

* Lots of java source code cleanup that won't affect the CFML experience, but will aid in faster development and fewer bugs.

#### 🐛Fixed

* Any hibernate exceptions returned during schema generation are once again logged to the Lucee ORM log file.

#### 💥 Removed

* Dropped the public method from the Dialect class. This method was unused (to my knowledge) and unnecessary.

#### 🔐 Security

* Switched to [Snyk vulnerability scanner](https://github.com/snyk/actions/tree/master/maven-3-jdk-11) to limit false positives. Security vulnerabilities will now be published on the [GitHub repository's Security Advisories page](https://github.com/Ortus-Solutions/extension-hibernate/security/advisories).
* Bumped Lucee dependency to to remove vulnerability notices on [org.apache.tika:tika-core](https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHETIKA-2936441) and [commons-net:commons-net](https://security.snyk.io/vuln/SNYK-JAVA-COMMONSNET-3153503). These vulnerabilities are only theoretical, since Lucee is a dependency and not bundled with the extension.

### [6.0.0](https://github.com/Ortus-Solutions/extension-hibernate/compare/b86f26e383ead941d18791e2e008cb62b2598cdc...6.0.0) - 2023-07-01

#### ⭐ Added

**Second-Level Caching**

The extension will now throw an error if you try to configure an unsupported cache provider like , , etc. Previously, the extension would silently switch to ehcache if any cache provider besides EHCache was configured.

**Hibernate Logging**

This version re-enables Hibernate logging via SLF4j and LogBack. Hibernate root and cache loggers are defaulted to level, while SQL logging is set to if is enabled. (Set to .)

**OWASP Dependency CVE Scans**

The extension [GitHub Release page](https://github.com/Ortus-Solutions/extension-hibernate/releases/latest) now generates a dependency CVE report via [Jeremy Long's OWASP dependency-check maven plugin](https://jeremylong.github.io/DependencyCheck/index.html). Any known CVEs contained in dependencies ( excluding and -scoped dependencies) will be noted in [each release's CVE report artifact](https://github.com/Ortus-Solutions/extension-hibernate/releases/download/latest/owasp-cve-report.html).

#### ♻️ Changed

**New Repo Layout**

* Java source moved to
* All java classes are now under the package
* Dropped the java source format-on-push in favor of format-on-save IDE tooling

**New Test Layout**

* Internal tests rewritten to native Testbox specs
* Cloned all ORM tests from the Lucee repository
* Updated to TestBox 5.0

**New Build (and .jar file) Layout**

We re-architected the build to inline most dependencies. I.e. we no longer copy in extension dependencies as (custom-built) OSGI bundles, but instead as compiled classes.

* This resolves intermittent issues with bundle resolution and/or duplicate bundle collision upon installing the ORM extension into a Lucee server prior to uninstalling the Lucee Hibernate extension.
* This also removes a number of direct dependencies on custom OSGI bundles, thus it is more reliable and will offer easier dependency upgrades with less pain.

**Other**

* The attribute is deprecated in Hibernate 5.x, and is no longer generated on HBM/XML mapping files to avoid Hibernate warning that Use of DOM4J entity-mode is considered deprecated.

#### 🐛Fixed

* The definition file for all built-ins was missed during the conversion to a Maven build. (Since [v5.4.29.25](https://github.com/Ortus-Solutions/extension-hibernate/releases/tag/v5.4.29.25)). This caused the and built-in method calls to be picked up by Lucee core before being routed to this extension. No known errors resulted from this mistake, but we feel embarrassed anyway. 😅
* Clear ORM context data once per ORM reload, not once per ORM entity parsing. This should improve ORM startup/reload time and avoid difficult session or cache manager lifecycle issues.
