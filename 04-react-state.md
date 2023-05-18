# React State

| Term | Definition |
| ---- | ---------- |
| __State__ | Refers to the data that represents the current condition or state of a component in a React application. It is mutable and can be updated over time. React components can have state to manage dynamic data and reflect changes in the user interface. |
| __Stateful__ | A stateful component, also known as a container component, is a React component that manages its own state. It keeps track of data that can change and affects the rendering of the component and its child components. |
| __Toggle__ | The action of alternating between two or more different options, states, or activities. In the context of the lesson, toggle is used to describe switching between different modes, such as switching between light mode and dark mode. |
| __Event Listeners__ | Functions or methods that wait for a specific event to occur, such as a button click or a keypress. They listen for these events and execute a designated code block or function (event handler) when the event occurs. |
| __Event Handlers__ | Functions that are invoked when a specific event, such as a button click or form submission, takes place. These functions define the behavior or actions that should be performed in response to the event. |
| __React Hooks__ | Functions that allow functional components to have state and perform side effects. They provide a way to use state and other React features without writing class components. The most commonly used hook for managing state is the `useState` hook. |
| __useState__ | A React hook that allows functional components to have state. It returns an array with two elements: the current state value and a function to update the state value. The initial state can be provided as an argument to useState. |
| __Class Components__ | The traditional way of creating components in React. They are JavaScript classes that extend the React.Component class and have a render method to define the component's UI. Class components can have state and lifecycle methods. _These have largely been replaced by Functional Components thanks to the introduction of React Hooks._ |
| __Initial State__ | The starting value or initial data of a component's state. It is the value that the state is set to when the component is first rendered or initialized. |
| __Updating State__ | Refers to modifying the value of a component's state after it has been initialized. It involves calling the appropriate function, such as `setState` or the function returned by the useState hook, to update the state with a new value. By updating state, React triggers a re-rendering of the component to reflect the updated state in the UI. |
| __Passed by reference__ | Arrays and objects are passed by reference in JavaScript. When you assign an array or object to a new variable, it points to the original array or object in memory. |

---

## Vanilla JavaScript event listener and handler

- What are some of the biggest challenges when writing event listeners and handlers in vanilla javascript? handlers have to be reset, we aslo have more to write out

```html
<!-- HTML -->
<div>
  <button>Change to dark mode</button>
</div>
```

```js
// JavaScript
const button = document.querySelector("button");
button.addEventListener("click", () => {
  console.log("Dark mode on!");
});
```

## React event listener and handler without arguments

- How does this differ from the vanilla js process? it looks more cleaner and is passed in jsx
- What is the `changeMode` function called? an event handler

```jsx
function App() {
  function changeMode() {
    console.log(`Color theme changed!`);
  }

  return (
    <div>
      <button onClick={changeMode}>Change to dark mode</button>
    </div>
  );
}
```

## React event listener and handler with arguments

- How does adding arguments change our event listener and event handler? it calls the function
- What is the arrow function doing inside of our `onClick`? It delays the function from being called until the event happens, because the parenthesis is added to the function it needs an anonymos funtion to delay it from being called.
- What is the arrow function called? Why is it called this? It is called an anonymous function and its called that because it has no name or parameter
- What would happen if you didn't include the arrow function? it would call the the function on load of the dom

```jsx
function App() {
  function changeMode(modeChoice) {
    console.log(`${modeChoice} is the best!`);
  }

  return (
    <div>
      <button onClick={() => changeMode("Dark mode")}>Change to dark mode</button>
    </div>
  );
}
```

## Creating state using React Hooks

- Why do we import `useState` inside of brackets? because it is a named function being imported from React and is not a default. 
- What does `mode` represent? Its the state (the way it starts) set by the destructing of useState and set in parenthesis.
- What does `setMode` represent? The way we are updating the value
- Why are we passing the string `'light'` to the `useState` hook? it sets the state

```jsx
import { useState } from "react";

function App() {
  const [mode, setMode] = useState('light');

  // Rest of the component code
}
```

## Updating state in React

- Why are we using an if statement here? Because we want to toggle between light and dark themes, basically definiing our options for updating state
- What is the `setMode` function doing? rerending mode, updating it and uses the brillance of react

```jsx
function changeMode(modeChoice) {
  if (mode === "light") {
    setMode("dark");
  } else {
    setMode("light");
  }
}
```

## Don't change state directly

- Why is it important to update the state using the helper functions provided by hooks rather than what we've grown used to in Vanilla JS?
because thats the whole point of react, to rerender quickly
```js
// You may find yourself tempted to do this:
mode = "light";

// Instead of
setMode("light");
```

## Copying an Array

- Does the spread operator make a shallow copy or a deep copy? It makes a shallow copy of the array 
- How can we use the process of copying an array to avoid changing state directly? we copy and then we update it how we want to [..somNumsAgain, 50, 60, 70, 80] is equal to [10, 20, 30, 40, 50, 60, 70, 80]
- What does the `reverse()` method do? reverse the array
- What will the two logs show?

```jsx
const someNumsAgain = [10, 20, 30, 40];
const copySomeNumsAgain = [...someNumsAgain];
copySomeNumsAgain.reverse();
console.log('Some nums again', someNumsAgain);
console.log('Copied some nums again', copySomeNumsAgain);
```

## Shallow Copies

- What happens to nested values in a shallow copy? it shares a memory space with the original
- What is this line `const newFido = { ...dog, name: "Fido Jr." };` doing? adding name: "Fido Jr." to a spread array
- What about this one `newFido.toys[0].name = "Super-sized bone";`?
- What will the logs of `dog` and `newFido` show? they both changed

```jsx
const dog = {
  name: "Fido",
  toys: [
    { name: "bone", cost: 6 },
    { name: "ball", cost: 4 },
    { name: "squeaky toy", cost: 8 },
  ],
};

const newFido = { ...dog, name: "Fido Jr." };
newFido.toys[0].name = "Super-sized bone";

console.log("Original dog");
console.log(dog);

console.log("new dog");
console.log(newFido);
```

## Deep Copying
//review this
- How does a deep copy differ from a shallow copy? we changed how we copy the the object, turning it into string with JSON.stringify() and then JSON.parse() to create deep copy
- What does `JSON.stringify()` do? turn it into strings
- What does `JSON.parse()` do? turnit back into data
- What will the logs of `dog` and `newFido` show? be different memory copies

```jsx
const dog = {
  name: "Fido",
  toys: [
    { name: "bone", cost: 6 },
    { name: "ball", cost: 4 },
    { name: "squeaky toy", cost: 8 },
  ],
};

const newFido = JSON.parse(JSON.stringify(dog));
newFido.toys[0].name = "Super-sized bone";

console.log("Original dog");
console.log(dog);

console.log("new dog");
console.log(newFido);
```
