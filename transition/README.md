# Transition


Here you can see we have a new component what will try to render our Github Search.

We are using a `mixins :[Router.History]`. Since we search something, it should
appear on the URL.

1.

```
<form onSubmit={this.handleSubmit}>
```

2.
```
handleSubmit: function(){
	var username = this.usernameRef.value;
	this.usernameRef.value = '';
	this.history.pushState(null, "profile/" + username)
},
```

3.
```
this.history.pushState(null, "profile/" + username)
```

Here some articles about pushState
http://jamesknelson.com/push-state-vs-hash-based-routing-with-react-js/


In the world of React.js single-page apps, there are two types of routing: push-state, and hash-based. Each of these have their strengths and weaknesses.


```
var React = require('react');
var Router = require('react-router');

var SearchGithub = React.createClass({
  mixins: [Router.History],
  getRef: function(ref){
    this.usernameRef = ref;
  },
  handleSubmit: function(){
    var username = this.usernameRef.value;
    this.usernameRef.value = '';
    this.history.pushState(null, "profile/" + username)
  },
  render: function(){
    return (
      <div className="col-sm-12">
        <form onSubmit={this.handleSubmit}>
          <div className="form-group col-sm-7">
            <input type="text" className="form-control" ref={this.getRef} />
          </div>
          <div className="form-group col-sm-5">
            <button type="submit" className="btn btn-block btn-primary">Search Github</button>
          </div>
        </form>
      </div>
    )
  }
});

module.exports = SearchGithub;
```
