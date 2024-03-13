---
description: How do Hibernate logs work in the Ortus ORM Extension?
---

# Logging

## How can I configure/acquire Hibernate logging in the Ortus ORM Extension?

The Ortus ORM Extension reconfigures all Hibernate logging output on startup to log `ERROR`-level events to the server console.

## How can I configure/acquire Hibernate logging in the Lucee Hibernate Extension?

This depends on the version of Lucee you are running - specifically, on whether you're on Log4J 2 or not.

### Lucee versions running Log4J 1.x

Lucee versions containing the older log4j 1.x can use this code to set a custom logging level and redirect the Hibernate logs to the server console:

```
void function setupHibernateLogging( level = "WARN" ){
	var Logger       = createObject( "java", "org.apache.log4j.Logger" );
	var log4jLevel   = createObject( "java", "org.apache.log4j.Level" );
	var hibernateLog = Logger.getLogger( "org.hibernate" );
	// set a custom log level
	hibernateLog.setLevel( log4jLevel[ arguments.level ] );

	/**
	 * Redirect all Hibernate logs to system.out
	 */
	if ( listFindNoCase( "Lucee", server.coldfusion.productname ) ) {
		var printWriter     = getPageContext().getConfig().getOutWriter();
		var layout          = createObject( "java", "lucee.commons.io.log.log4j.layout.ClassicLayout" );
		var consoleAppender = createObject( "java", "lucee.commons.io.log.log4j.appender.ConsoleAppender" ).init(
			printWriter,
			layout
		);
		hibernateLog.addAppender( consoleAppender );
		writeDump( var = "** Lucee Hibernate Logging Redirected", output = "console" );
	}
}
```

### Lucee versions running Log4J 2.x

For versions of Lucee running log4j 2.x, the above workaround does not apply. If you are interested in tweaking the Hibernate logging level in the Lucee Hibernate extension, I would suggest [sponsoring this feature](https://www.ortussolutions.com/products/orm-extension#support) and future users can benefit from the shared knowledge.
