# State and Props

## Props

Passing Variables to Components:

```javascript
<Route path="profile/:username" component={Profile} />
```

Look at this Component:

We are getting the variable using `this.props.variable_name`.

```javascript
var React = require('react');

var Notes = React.createClass({
  render: function(){
    return (
      <div>
        <p>NOTES </p>
        <p> {this.props.notes}</p>

      </div>
    )
  }
})

module.exports = Notes;
```

Do not forget to export the Module by using `module.exports = Notes`.


## State

At this example, you can check how to use state.

```javascript
var Profile = React.createClass({
  getInitialState: function(){
    return {
      notes: [1,2,3],
      bio: {
        name: 'Tyler McGinnis'
      },
      repos: ['a', 'b', 'c']
    }
  },
  render: function(){
    console.log(this.props)
    return (
      <div className="row">
        <div className="col-md-4">
          <UserProfile username={this.props.params.username} bio={this.state.bio} />
        </div>
        <div className="col-md-4">
          <Repos repos={this.state.repos}/>
        </div>
        <div className="col-md-4">
          <Notes notes={this.state.notes} />
        </div>
      </div>
    )
  }
})
```
