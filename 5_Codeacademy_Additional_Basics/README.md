# REACT STYLES :

+ Inline Styles :

```html
<h1 style={{ color: 'red' }}>Hello world</h1>
```
+ Style Object Variables :

```javascript
const darkMode = {
  color: 'white',
  background: 'black';
};

<h1 style={darkMode}>Hello world</h1>
```

+  in JavaScript, we write CSS property names using camelCase in React:
```javascript
const styles = {
  marginTop: '20px',
  backgroundColor: 'green'
};
```

+ If you write a style value as a number, then the unit 'px' is assumed. For example, if you want a font size of 30px, you can write:

  `{ fontSize: 30 }`

+ If you want to use units other than 'px', you can use a string:

  `{ fontSize: "2em" }`


