# Data Persistence

Here we will see some aspects of the life cycle.

Basically, we will use these two methods for bind the notes array with something
coming from our API.


```javascript
componentDidMount: function(){
	this.ref = new Firebase('https://github-note-taker.firebaseio.com/');
	var childRef = this.ref.child(this.props.params.username);
	this.bindAsArray(childRef, 'notes');
},
componentWillUnmount: function(){
	this.unbind('notes');
},
```

### Mounting: componentDidMount
void componentDidMount()
Invoked once, only on the client (not on the server), immediately after the initial rendering occurs. At this point in the lifecycle, you can access any refs to your children (e.g., to access the underlying DOM representation). The componentDidMount() method of child components is invoked before that of parent components.

If you want to integrate with other JavaScript frameworks, set timers using setTimeout or setInterval, or send AJAX requests, perform those operations in this method.


### Unmounting: componentWillUnmount #
void componentWillUnmount()
Invoked immediately before a component is unmounted from the DOM.

Perform any necessary cleanup in this method, such as invalidating timers or cleaning up any DOM elements that were created in componentDidMount.
