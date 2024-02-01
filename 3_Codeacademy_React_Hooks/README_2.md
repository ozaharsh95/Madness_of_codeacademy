## THE EFFECT HOOK :

+ we’ll use the Effect Hook to run some JavaScript code after each render to:

   + fetch data from a back-end service.
   + subscribe to a stream of data.
   + manage timers and intervals.
   + read from and make changes to the DOM.

+ There are three key moments when the Effect Hook can be utilized:

    1. When the component is first added, or mounted, to the DOM and renders.
    2. When the state or props change, causing the component to re-render.
    3. When the component is removed, or unmounted, from the DOM.

+ The Effect Hook tells our component to do something every time it’s rendered (or re-rendered). Combined with states, we can use the Effect Hook to create interesting dynamic changes in our web pages!

+ The `useEffect()` function has no return value as the Effect Hook is used to call another function. We pass the callback function, or effect, to run after a component renders as the argument of the `useEffect()` function. 

## Clean Up Effects :

+ When we add event listeners to the DOM, it is important to remove those event listeners when we are done with them to avoid memory leaks!

+ Let’s consider the following effect:
```javascript
useEffect(()=>{
  document.addEventListener('keydown', handleKeyPress);
  // Specify how to clean up after the effect:
  return () => {
    document.removeEventListener('keydown', handleKeyPress);
  };
})
```

+ If our effect didn’t return a cleanup function, a new event listener would be added to the DOM’s document object every time that our component re-renders. Not only would this cause bugs, but it could cause our application performance to diminish and maybe even crash!

+ If our effect returns a function, then the `useEffect()  ` Hook always treats that as the cleanup function. React will call this cleanup function before the component re-renders or unmounts. Since this cleanup function is optional, it is our responsibility to return a cleanup function from our effect when our effect code could create memory leaks.


## Control When Effects Are Called :

+ It is common, when defining function components, to run an effect only when the component mounts (renders the first time), but not when the component re-renders. The Effect Hook makes this very easy for us to do! If we want to only call our effect after the first render, we pass an empty array to `useEffect()` as the second argument. This second argument is called **the dependency array**.

+ The dependency array is used to tell the `useEffect()` method when to call our effect and when to skip it. Our effect is always called after the first render but only called again if something in our dependency array has changed values between renders.

+ The dependency array is used to tell the `useEffect()` method when to call the effect.

    1. By default, with no dependency array provided, the effect is called after every render.
    
    2. An empty dependency array signals that the effect never needs to be re-run.
    
    3. A non-empty dependency array signals that the hook runs the effect only when any of the dependency array values changes.

```javascript
useEffect(() => {
 alert('called after every render');
});
 
useEffect(() => {
 alert('called after first render');
}, []);
 
useEffect(() => {
 alert('called when value of `endpoint` or `id` changes');
}, [endpoint, id]);
```

## Fetch Data :

+ When the data that our components need to render doesn’t change, we can pass an empty dependency array so that the data is fetched after the first render. 

+ When the response is received from the server, we can use a state setter from the State Hook to store the data from the server’s response in our local component state for future renders. 

+ Using the State Hook and the Effect Hook together in this way is a powerful pattern that saves our components from unnecessarily fetching new data after every render!

+ An empty dependency array signals to the Effect Hook that our effect never needs to be re-run, that it doesn’t depend on anything. 

+ Specifying zero dependencies means that the result of running that effect won’t change and calling our effect once is enough.

## Rules of Hooks :

+ There are two main rules to keep in mind when using hooks:

    1. Only call hooks from React function components.
    2. Only call hooks at the top level, to be sure that hooks are called in the same order each time a component renders.
    3. Common mistakes to avoid are calling hooks inside of loops, conditions, or nested functions.

```javascript
// Instead of confusing React with code like this:
if (userName !== '') {
 useEffect(() => {
   localStorage.setItem('savedUserName', userName);
 });
}

// We can accomplish the same goal, while consistently calling our hook every time:
useEffect(() => {
 if (userName !== '') {
   localStorage.setItem('savedUserName', userName);
 }
});
```

## Multiple Effect Hooks

+ `useEffect()` may be called more than once in a component. This gives us the freedom to individually configure our dependency arrays, separate concerns, and organize the code.
```javascript
function App(props) {
 const [title, setTitle] = useState('');
 useEffect(() => {
   document.title = title;
 }, [title]);
 
 const [time, setTime] = useState(0);
 useEffect(() => {
   const intervalId = setInterval(() => setTime((prev) => prev + 1), 1000);
   return () => clearInterval(intervalId);
 }, []);
  

}
```