# Events

Hibernate ORM allows reacting to various events in the session lifecycle such as `onPreInsert`, `onPostUpdate`, `onFlush`, etc. To enable listening to these events, set `eventHandling` to `true` and pass a path to the global event handler using `eventHandler`:

```js
this.ormSettings = {
    eventHandling: true,
    eventHandler : "path/to/global/EventHandler.cfc"
};
```

The `EventHandler.cfc` must then contain function definitions matching the ORM events you wish to listen for.

Currently, the available event names are:

* `onFlush`
* `postNew`
* `preLoad`
* `postLoad`
* `preInsert`
* `postInsert`
* `preUpdate`
* `postUpdate`
* `preDelete`
* `onDelete`
* `postDelete`
* `onEvict`
* `onClear`
* `onDirtyCheck`
* `onAutoFlush`

Here's an example of an EventHandler configured for all events:

```js
component {

	public component function init(){
		return this;
	}

	function onFlush( entity ) {
		// Do something upon function call
	}

	function postNew( any entity, any entityName ){
		// Do something upon function call
	}

	function preLoad( entity ){
		// Do something upon function call
	}
	function postLoad( entity ){
		// Do something upon function call
	}

	function preInsert( entity ){
		// Do something upon function call
	}
	function postInsert( entity ){
		// Do something upon function call
	}

	function preUpdate( entity, Struct oldData  ){
		// Do something upon function call
	}
	function postUpdate( entity ){
		// Do something upon function call
	}

	function preDelete( entity ){
		// Do something upon function call
	}	
	function onDelete( entity ) {
		// Do something upon function call
	}
	function postDelete( entity ) {
		// Do something upon function call
	}

	function onEvict() {
		// Do something upon function call
	}
	function onClear( entity ) {
		// Do something upon function call
	}
	function onDirtyCheck( entity ) {
		// Do something upon function call
	}
	function onAutoFlush( entity ) {
		// Do something upon function call
	}
}
```
