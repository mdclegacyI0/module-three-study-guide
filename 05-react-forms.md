# React Forms

| Term | Definition |
| ---- | ---------- |
| __Controlled components__ | React inputs that are controlled by React state, ensuring that the state and view are synchronized. |
| __Uncontrolled components__ | Inputs in React that are not explicitly controlled by React, meaning their state is managed by the browser rather than React. |

---

## Checkboxes

- What is `checked={checked}` doing? passing our state to the input component
- What is `setChecked(!checked)` doing? setting state to the opposite of what it currently is
- What happens if we forget the `onChange` event listener? no change wil occur to the original state, we will see an error in the console. 
- What's controlling the checkbox: React or the Browser? React is controlling it, our state is telling what to do.

```js
// State
const [checked, setChecked] = useState(false);

// Event Handler
function handleCheckboxChange() {
  setChecked(!checked);
}

// JSX
<input type="checkbox" checked={checked} onChange={handleCheckboxChange} />
```

## Select Dropdowns

- What is the default value of `selectOption`? Why? an empty string ("") because its equal to the initial state
- Why are we setting the `selectOption` to `event.target.value`? because we want to know the value selected and update the state using that value
- The option value `cats` doesn't match the option display `Cats!`. Is that ok? Thats ok because (Cats!) is just the name shown to the user

```js
// State
const [selectOption, setSelectOption] = useState("");

// Event Handler
function handleSelectChange(event) {
  setSelectOption(event.target.value);
}

// JSX
<select value={selectOption} onChange={handleSelectChange}>
  <option value=""></option>
  <option value="cats">Cats!</option>
  <option value="dogs">Dogs!</option>
</select>
```

## Text Inputs

- What is missing from this text input? A value for this example. i'll add it! *added (it would also need an id and name in real world uses)
- When does the `onChange` event trigger? It triggers the function that updates the name to the value of the event

```js
// State
const [nickName, setNickName] = useState("");

// Event Handler
function handleNickNameChange(event) {
  setNickName(event.target.value);
}

// JSX
<input value={nickName} type="text" onChange={handleNickNameChange} />
```

## Form Submission

- When does the `onSubmit` event trigger?the sumbit event of the form, it validates information
- What does `event.preventDefault()` do? It prevents the page from reseting, refreshing and passing input values and names to the query string in the url. *The preventDefault() method of the Event interface tells the user agent that if the event does not get explicitly handled, its default action should not be taken as it normally would be.

```jsx
// Event Handler
function handleSubmit(event) {
  event.preventDefault();
  console.log("form submitted");
}

// JSX
<form onSubmit={handleSubmit}>
  <input type="submit" />
</form>
```

## Multiple text inputs with a shared change handler

- What data type is the `user` state? It is an Object
- Why are we using curly braces when we invoke `setUser({...})`? because it creates a new object, to add new values and ids of the event 
- What does `...user` accomplish? its spreads  all the values of the original object
- What's is this `[event.target.id]: event.target.value` doing? get me the target of the new event that happened, submit
- What other input attribute could you use instead of `id`? 

```js
// State
const [user, setUser] = useState({
  firstName: "",
  lastName: "",
  zip: "",
  email: "",
  password: "",
});

// Event Handler
function handleTextChange(event) {
  setUser({
    ...user,
    [event.target.id]: event.target.value,
  });
}

// JSX
<form onSubmit={handleSubmit}>
  <input type="text" value={user.firstName} onChange={handleTextChange} id="firstName" />
  <input type="text" value={user.lastName} onChange={handleTextChange} id="lastName" />
  <input type="number" value={user.zip} onChange={handleTextChange} id="zip" />
  <input type="email" value={user.email} onChange={handleTextChange} id="email" />
  <input type="password" value={user.password} onChange={handleTextChange} id="password" />
  <input type="submit" />
</form>
```

## Resetting the form

- What is the `resetForm()` doing to the state?
- Are we updating the object directly? How can you tell?

```js
function resetForm() {
  setUser({
    firstName: "",
    lastName: "",
    zip: "",
    email: "",
    password: "",
  });
}

function handleSubmit(event) {
  event.preventDefault();
  console.log("form submitted");
  resetForm();
}
```
