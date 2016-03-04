# Stateless Functional Components

One feature for React 0.14 is Stateless Functional Components
https://facebook.github.io/react/blog/2015/10/07/react-v0.14.html#stateless-functional-components


In idiomatic React code, most of the components you write will be stateless, simply composing other components. We’re introducing a new, simpler syntax for these components where you can take props as an argument and return the element you want to render:


```
// A functional component using an ES2015 (ES6) arrow function:
var Aquarium = (props) => {
  var fish = getFish(props.species);
  return <Tank>{fish}</Tank>;
};

// Or with destructuring and an implicit return, simply:
var Aquarium = ({species}) => (
  <Tank>
    {getFish(species)}
  </Tank>
);

// Then use: <Aquarium species="rainbowfish" />
```


These components behave just like a React class with only a render method defined. Since no component instance is created for a functional component, any ref added to one will evaluate to null. Functional components do not have lifecycle methods, but you can set .propTypes and .defaultProps as properties on the function.

This pattern is designed to encourage the creation of these simple components that should comprise large portions of your apps. In the future, we’ll also be able to make performance optimizations specific to these components by avoiding unnecessary checks and memory allocations.
