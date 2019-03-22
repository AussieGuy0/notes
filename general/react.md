# React

## Concepts

### Components
A component takes in parameters (`props`) and returns a view through the
`render` function. The `render` function returns a `React Element`, which is
often accomplished by using `jsx` syntax. You could also just use
`React.createElement()`.

```jsx
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}

// Example usage: <ShoppingList name="Mark" />
```

We can add state to a component by initializing a `state` object in the
component's constructor. We can then use `setState` to change this state object.
When `setState` is called, React will re-render the component. This means that
React components are immutable!

```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    }
  }
  
  render() {
    return (
      <div>
        <span>{this.state.count}</span>  
        <button onClick={() => this.setState({count: this.state.count + 1})>+</button>
      </div>
    )
  }
}
```

**Important note about child/parent communication**: To collect data from multiple children, 
or to have two child components communicate with each other, you need to declare the shared 
state in their parent component instead. The parent component can pass the state back down 
to the children by using props; this keeps the child components in sync with each other 
and with the parent component.

#### Function Components
If we only need a component with a `render` method with no state, we can use the
simplier 'Fuction Component'. Function Components are much simplier than normal
'Class' Components.

Class component example:
```jsx
class Square extends React.Component {
  render() {
    return (
      <button 
        className="square"
        onClick={this.props.onClick}>
        {this.props.value}
      </button>
    );
  }
}
```

Equivilant function component:
```jsx
function Square(props) {
    return (
      <button 
        className="square"
        onClick={props.onClick}>
        {props.value}
      </button>
    );
}
```


### JSX
JSX is a extension of the javascript language. It basically allows us to write
HTML within javascript. More specifically, it allows an easier syntax for us to
create 'React Elements'.

Here is an example:

```jsx
const name = "John";
const element = <h1>Hello, {name}</h1>;
```

Any valid javascript can exist within the `{}` braces.

We can use javascript to apply an attribute to an element

```jsx
const element = <img src={user.avatarUrl}></img>;
```

**NOTE**: We have use *camelCase* attribute names ('tabIndex' instead of
'tabindex'). Also, since `class` is a reserved keyword in javascript, we 
need to have use `className`.

### Immutability
React heavily encourages the idea of immutability. Basically, instead of
mutating state, we should be replacing the state.

By having immutable components, React can have better knowledge on whether a
components needs to re-render. 



## Useful Links
[React Offical Tutorial](https://reactjs.org/tutorial/tutorial.html#overview)
[JSX Explained](https://reactjs.org/docs/introducing-jsx.html)
