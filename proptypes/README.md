# PropTypes

As your app grows it's helpful to ensure that your components are used correctly. We do this by allowing you to specify propTypes

### Example of PropTypes

```java
var Notes = React.createClass({
  propTypes: {
    username: React.PropTypes.string.isRequired,
    notes: React.PropTypes.array.isRequired
  },
  render: function(){
    return (
      <div>
        <h3> Notes for {this.props.username} </h3>
        <NotesList notes={this.props.notes} />
      </div>
    )
  }
})

module.exports = Notes;
```
