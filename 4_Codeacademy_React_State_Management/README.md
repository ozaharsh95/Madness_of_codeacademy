# Learn React: State Management :
# REACT PROGRAMMING PATTERNS :
## Separate Container Components From Presentational Components :

+ **Stateful and Stateless Components** :

    + In React, a stateful component is a component that holds some state. Stateless components, by contrast, have no state. Note that both types of components can use props.

    + In the example, there are two React components. The Store component is stateful and the Week component is stateless.

```javascript
//stateful

function Store() {
  const [sell, setSell] = useState("anything");

  
  return <h1>I'm selling {sell}.</h1>;
  
}

//stateless
function Week(props){
  
  return <h1>Today is {props.day}!</h1>;
  
}
```

+ React Programming Pattern :

+ One of the most common programming patterns in React is to use stateful parent components to maintain their own state and pass it down to one or more stateless child components as props. The example code shows a basic example.

```javascript

// This is a stateful Parent element.
// Container Component
function Yoda() {
  const [ name, setName ] = useState("Toyoda")

  // The child component will render information passed down from the parent component.
  return <BabyYoda name={name} />;
  
}

// This is a stateless child component.
// Presentational Component
function BabyYoda(props) {
  return <h2>I am {props.name}!</h2>;
}
```

+ Identified that the original component needed to be refactored: it handled calculations/logic and presentation/rendering.
+ Created a container component containing all the stateful logic.

+ Created a function that calls the state setter method provided by useState().

+ Created and exported presentational components containing only JSX.

+ Imported the presentational components into the container component.

+ Used the presentational components in the return statement of the container component.

+ Passed state and functions used to change state as props to the rendered presentational components.