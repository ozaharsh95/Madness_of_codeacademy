# REACT HOOKS :

+ Using Hooks, we can determine what we want to show the users by declaring how our user interface should look based on the state.

## THE STATE HOOK :

+ `import {useState} from 'react';`

+ `useState()` fxn returns two values :
    1. The current state: The current value of this state.
    2. The state setter: A function that we can use to update the value of this state.

+ To extract the two values from the array, we can assign them to local variables by using array destructuring. For example:

  `const [currentState, setCurrentState] = useState();`

```javascript
  //example 1:
import React, { useState } from "react";

function Toggle() {
  const [toggle, setToggle] = useState();

  return (
    <div>
      <p>The toggle is {toggle}</p>
      <button onClick={() => setToggle("On")}>On</button>
      <button onClick={() => setToggle("Off")}>Off</button>
    </div>
  );
}
```
+ There are three ways in which this code affects our component:

  1. During the first render, the initial state argument is used.
  2. When the state setter is called, React ignores the initial state argument and uses the new value.
  3. When the component re-renders for any other reason, React continues to use the same value from the previous render.

+ jo apade initial value pass na kariye to by default `undefined` hoy chhe.


### Use State Setter Outside of JSX :


```javascript
//example 2
import React, { useState } from 'react';

export default function EmailTextInput() {
  const [email, setEmail] = useState('');
  const handleChange = (event) => {
    const updatedEmail = event.target.value;
    setEmail(updatedEmail);
  }

  return (
    <input value={email} onChange={handleChange} />
  );
}

```
+ Earlier in this lesson, we wrote our event handlers right in our JSX (in example 1). Those inline event handlers work perfectly fine, but when we want to do something more interesting than just calling the state setter with a static value, it’s a good practice to separate that logic from our JSX. This separation of concerns makes our code easier to read, test, and modify.

+ Simplification of code

```js
//changing this
const handleChange = (event) => {
  const newEmail = event.target.value;
  setEmail(newEmail);
}

👇👇👇👇👇👇👇
// to this
const handleChange = (event) => setEmail(event.target.value);

👇👇👇👇👇👇👇
//or this also
const handleChange = ({target}) => setEmail(target.value);

```

### Set From Previous State :

+ It is best practice to update a state with a callback function, preventing accidental outdated values.

```js
import React, { useState } from 'react';
 
export default function Counter() {
  const [count, setCount] = useState(0);
 
  const increment = () => setCount(prevCount => prevCount + 1);
 
  return (
    <div>
      <p>Wow, you've clicked that button: {count} times</p>
      <button onClick={increment}>Click here!</button>
    </div>
  );
}

```

### Arrays in State :

+ Array,objects pan use thay useState ma.
+ [Array Lesson Link](https://www.codecademy.com/courses/learn-react-hooks/lessons/the-state-hook/exercises/arrays-in-state)
```js
// Array example :
import React, { useState } from 'react';

//Static array of pizza options offered. 
const options = ['Bell Pepper', 'Sausage', 'Pepperoni', 'Pineapple'];

export default function PersonalPizza() {
  const [selected, setSelected] = useState([]);

  const toggleTopping = ({target}) => {
    const clickedTopping = target.value;
    setSelected((prev) => {
     // check if clicked topping is already selected
      if (prev.includes(clickedTopping)) {
        // filter the clicked topping out of state
        return prev.filter(t => t !== clickedTopping);
      } else {
        // add the clicked topping to our state
        return [clickedTopping, ...prev];
      }
    });
  };

  return (
    <div>
      {options.map(option => (
        <button value={option} onClick={toggleTopping} key={option}>
          {selected.includes(option) ? 'Remove ' : 'Add '}
          {option}
        </button>
      ))}
      <p>Order a {selected.join(', ')} pizza</p>
    </div>
  );
}

```
+ [Object Lesson Link](https://www.codecademy.com/courses/learn-react-hooks/lessons/the-state-hook/exercises/objects-in-state)

```js
//Object example
export default function Login() {
  const [formState, setFormState] = useState({});
  const handleChange = ({ target }) => {
    const { name, value } = target;
    setFormState((prev) => ({
      ...prev,
      [name]: value
    }));
  };

  return (
    <form>
      <input
        value={formState.firstName}
        onChange={handleChange}
        name="firstName"
        type="text"
      />
      <input
        value={formState.password}
        onChange={handleChange}
        type="password"
        name="password"
      />
    </form>
  );
}

```