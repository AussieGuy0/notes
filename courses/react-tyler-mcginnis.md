# React by Tyler Mcginnis
https://tylermcginnis.com/courses/react/

## React Overview
- React takes the idea of composable functions and applies it to UI. As
  composition is common in all lanugages, the same intuition can be directly 
  applied to building React components.
- Since it's 'just' Javascript, there's a lot less API to learn compared to
  something like Vue and Angular.
- Learning React isn't the difficult part, it's learning how the ecosystem
  (e.g. libaries) fit together.
- Important libaries: React Router, Styled Components, Redux.
- If you're a beginner to React: don't use Redux. There's even a chance that
  you won't need to use redux.
- (Bonus) Composition vs Inheritance is a good article!

## The Road To Hello World
- NPM dependency version:
    - "^15.7.2" - Newest version with same major version
    - "~15.6.1" - Newest version with same major **and** minor version 
    - "15.7.2"  - Exact version
- When learning a new tool ask yourself 2 questions:
    - Why does this tool exist?
    - What problems does this tool solve?
- Webpack
    - Loaders: Allow webpack to process more than just JS and JSON files
    - Plugins: Allow webpack to execute certain tasks after the bundle has been
      created
    - Seeing mode to production will set `process.env.NODE_ENV` to production in
      app and minify code.
- Why is React split from ReactDOM?
  - React could be used in different environments (e.g. Mobile)
- (Generally) only one `ReactDOM.render` per React application. This render will
  point to the 'root' component, which will be used to render all the other
  components in the application.

## React Element vs React Component
- Elements:
- 
```js
    React.createElement('div', {id: 'login-btn'}, 'Login')
    
    // Will return an object:
    
    {
        type: 'div',
        props: {
            children: 'Login',
            id: 'login-btn'
        }
    }
```

- A component is a function or a Class which may accept input and returns a
  React element
  
### JSX
- Expressions need to be wrapped in curly braces
```js
class App extends React.Component {
    return (
        <span>What is 2 + 2? {2 + 2}</span> 
    );
}
```
- Can only return one top level elemnt , unless you use `React.Fragment`
- React components have to start with an uppercase. This is how React differs
  built in HTML elements to custom React components.
  

## Passing Data to Components
- Props are to components what arguments are to functions
- You can access props in a component with `this.props`.
- Example
```js
var USER_DATA = {
  name: 'Tyler McGinnis',
  img: 'https://avatars0.githubusercontent.com/u/2933430?v=3&s=460',
  username: 'tylermcginnis'
}

class Badge extends React.Component {
  render() {
    console.log(this.props)
    return (
      <div>
        <img src={this.props.user.img} />
        <h1>Name: {this.props.user.name} </h1>
        <h3>username: {this.props.user.username} </h3>
      </div>
    )
  }
}

ReactDOM.render(
  <Badge user={USER_DATA}/>,
  document.getElementById('app')
);
```

## Rendering Lists in React
```js
// We provide a 'key' to list element to help React to know which items have
// changed during renders
<ul id="tweets">
    {tweets.map((tweet) => (
        <li key={tweet.id}> 
            {tweet.text}
        </li>
    ))}
</ul>
```
  
## Meta Course Notes
- I really like his focus of slow, fundamentals-first focus on learning. I feel
  like courses skip stuff to get you to the other end as quick as possible.
