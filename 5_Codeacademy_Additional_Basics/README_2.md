# REACT FORMS:

+ In a React form, you want the server to know about every new character or deletion, as soon as it happens. That way, your screen will always be in sync with the rest of your application.

## input onChange :

+ In a regular HTML form, the state of the form is typically managed by the browser. It doesn’t update the server until the user hits submit.

+ Things work a bit differently in React. In a React form, the state of the form can be managed by the component, and updates are triggered by the onChange event. When the user interacts with an input, such as entering or deleting any characters, the onChange event fires and updates the component state.

+ This allows the component to immediately reflect any changes made by the user and update the view accordingly.

## controlled and uncontrolled components :