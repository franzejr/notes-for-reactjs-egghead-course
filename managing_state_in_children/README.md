# Managing State in Children

Now we will try to manipulate the state of all three components.
What we need to do is pass and manipulate the state once a new change
has been made.

Profile.js

```javascript
var React = require('react');
var Router = require('react-router');
var Repos = require('./Github/Repos');
var UserProfile = require('./Github/UserProfile');
var Notes = require('./Notes/Notes');
var ReactFireMixin = require('reactfire');
var Firebase = require('firebase');

var Profile = React.createClass({
  mixins: [ReactFireMixin],
  getInitialState: function(){
    return {
      notes: [1,2,3],
      bio: {
        name: 'Tyler McGinnis'
      },
      repos: ['a', 'b', 'c']
    }
  },
  componentDidMount: function(){
    this.ref = new Firebase('https://github-note-taker.firebaseio.com/');
    var childRef = this.ref.child(this.props.params.username);
    this.bindAsArray(childRef, 'notes');
  },
  componentWillUnmount: function(){
    this.unbind('notes');
  },
  handleAddNote: function(newNote){
    this.ref.child(this.props.params.username).child(this.state.notes.length).set(newNote)
  },
  render: function(){
    return (
      <div className="row">
        <div className="col-md-4">
          <UserProfile username={this.props.params.username} bio={this.state.bio} />
        </div>
        <div className="col-md-4">
          <Repos username={this.props.params.username} repos={this.state.repos}/>
        </div>
        <div className="col-md-4">
          <Notes
            username={this.props.params.username}
            notes={this.state.notes}
            addNote={this.handleAddNote} />
        </div>
      </div>
    )
  }
})

module.exports = Profile;
```

Take a new note and then, update Firebase with a new Note.
Because you have bind the notes, once a change it will update the note in all the page.

The key point here is the binding of the Array and the function you can see above:

```javascript
handleAddNote: function(newNote){
	this.ref.child(this.props.params.username).child(this.state.notes.length).set(newNote)
},
```


## Notes

Let's create the PropType because it will be required.

```javascript
var React = require('react');
var NotesList = require('./NotesList');
var AddNote = require('./AddNote');

var Notes = React.createClass({
  propTypes: {
    username: React.PropTypes.string.isRequired,
    notes: React.PropTypes.array.isRequired,
    addNote: React.PropTypes.func.isRequired,
  },
  render: function(){
    return (
      <div>
        <h3> Notes for {this.props.username} </h3>
        <AddNote username={this.props.username} addNote={this.props.addNote} />
        <NotesList notes={this.props.notes} />
      </div>
    )
  }
})

module.exports = Notes;
```
