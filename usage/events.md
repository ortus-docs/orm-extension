---
description: Easily run actions on entity insertion, update, and more with event listeners
---

# Events

Hibernate ORM allows reacting to various events in the session lifecycle such as `onPreInsert`, `onPostUpdate`, `onFlush`, etc. You can enable event handling in CFML by setting `eventHandling` to `true` in your `this.ormSettings` struct:

```js
this.ormSettings = {
    eventHandling: true
};
```

This will enable two different event listener types for listening to Hibernate events:

* Listen to all events across all entities via the [global event handler](#global-event-handler)
* Listen to specific events on a specific entity via [entity event handler](#entity-event-handler) methods

## Global Event Handler

To use a global event handler, you must set a path to the global event handler using the `eventHandler` setting:

```js
this.ormSettings = {
    eventHandling: true,
    eventHandler : "path/to/global/EventHandler.cfc"
};
```

The `EventHandler.cfc` must then contain function definitions matching the ORM events you wish to listen for.

Currently, the available event names are:

* `onFlush`
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

## Entity Event Handler

You can also listen to events on a specific entity at the entity level by adding methods to the entity (component) itself:

```js
component persistent="true"{
	function preInsert( entity ){
		setDateCreated( now() );
	}
	function preUpdate( entity ){
		setDateModified( now() );
	}
}
```

{% hint style="info" %}
Note that only events related to a specific entity will fire upon that entity. For example, you cannot listen to `onFlush` in an entity event handler because a flush is not tied to any one entity.
{% endhint %}

Here is the full list of event types which can be listened to in entity event listeners:

* `preLoad`
* `postLoad`
* `preInsert`
* `postInsert`
* `preUpdate`
* `postUpdate`
* `preDelete`
* `onDelete`
* `postDelete`