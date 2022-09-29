# React

---

## Anatomy

> What are all the files in a React Project?

There are many ways to start a **React App**, including:

- Create React App
- Vite
- Next.js

### Create React App

To use **Create React App** simply type in the cmd line:

```bash .numberLines
npx create-react-app
```

The **Create React App** tool manages a _webpack_ behind the scenes so you dont have to.

#### Webpack:

> Webpack is a module bundler that is responsible for combining all of your javascript code into a single file that can be used by a web browser.

### Files & File Structure

#### Tree:

```text
📦react-base
 ┣ 📂node_modules
 ┣ 📂public
 ┃ ┣ 📜favicon.ico
 ┃ ┣ 📜index.html
 ┃ ┣ 📜logo192.png
 ┃ ┣ 📜logo512.png
 ┃ ┣ 📜manifest.json
 ┃ ┗ 📜robots.txt
 ┣ 📂src
 ┃ ┣ 📜index.js
 ┃ ┗ 📜index.scss
 ┣ 📜.gitignore
 ┣ 📜package-lock.json
 ┣ 📜package.json
 ┗ 📜README
```

#### Files / Folders:

##### package.json

> The _package.json_ is where your installed dependencies are listed.

##### public/

> The public folder houses static files and the html shell for your website.

##### index.js

> The _index.js_ file is the initial entrypoint for the web app and tells the React App how to start up.

##### App.js

> The first actual React Component is the _App.js_

Component files, like this one, often end in the _.js_ or the _.jsx_ file extension.
It's a good practice to only export **one** component from **one** file.

---

## Components

> Reusable pieces of UI that are composed together as a tree to represent a complete front end application.

### Defining a component with JSX

A component can be in the structure of a **function**, a **class**, or an **arrow function**.

```jsx .numberLines
/* Function Declaration */
function MyComponent() {
  return (
    <p>Hello, World!</p>;
  )
}

/* Function Expression / Arrow Function */
const MyComponent = () => {
  return (
    <p>Hello, World!</p>
  )
}

/* Class extending React.Component */
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    /* code... */
  }
  render() {
    return (
      <p>Hello, World!</p>
    )
  }
}

<MyComponent />
```

<br />

### Share Data with Props

A prop can be a primitive value like a string or number, and object, or even another React component.

```jsx .numberLines
function MyComponent(props) {
  return <p>Hello, {props.name}!</p>
}

<MyComponent name="Parker" />

/* Deconstructing to pass props */
function MyComponent({ name }) {
  return <p>Hello, {name}!</p>
}

<MyComponent name={'Parker Cole' + 24}>
```

To make a **container, or (shell like)** component, (similiar to Angulars `<ng-content></ng-content>`), you must pass in **props.children**:

##### Example

~ _App.js_

```jsx .numberLines
import React from 'react';
import '../styles.css';

function Card(props) {
	return (
		<section>
			<h2>{props.icon}</h2>
			{props.children}
		</section>
	);
}

function MyIcon() {
	return <i>🔥</i>;
}

export default function App() {
	return (
		<div>
			<Card icon={<MyIcon />} />
			<p>The body of the card</p>
		</div>
	);
}
```

## Conditional Rendering

> **Conditional rendering** is a very common pattern where you render a component based on a boolean condition. There are several ways to implement conditional rendering in React.

You have **3 Options**:

### Option 1: IF ELSE

```jsx .numberLines
function Conditional({ count }) {
	if (count > 5) {
		return <h1>Count is greater than 5</h1>;
	} else {
		return <h1>Count is less than 5</h1>;
	}
}
```

### Option 2: TERNARY

```jsx .numberLines
function Conditional({ count }) {
  return (
    {count % 2 === 0 ? <h1>Count is even</h1> : <h1>Count is odd</h1> }
  )
}
```

### Option 3: LOGICAL AND (&&)

```jsx .numberLines
function Conditional({ count }) {
  return (
    {count && 2 === 0 ? <h1>Count is even</h1> }
  )
}
```

## Loops

```jsx .numberLines
function ListOfAnimals() {
const data = [
  { id: 1, name: 'Fido 🐕' },
  { id: 2, name: 'Snowball 🐈' },
  { id: 3, name: 'Murph 🐈‍⬛' },
  { id: 4, name: 'Zelda 🐈' },
];

function ListOfAnimals() {
  return (
    <ul>
      {data && // Only render if there's data - see 'Conditional Rendering'
        data.map(({ id, name }) => {
          return <li key={id}>{name}</li>;
        })}
    </ul>
  );
}
```

## Events

#### Events In React

```jsx .numberLines
function Events() {
	return <button onClick={(event) => console.log(event)}></button>;
}
```

##### Example:

> Implement a text input that updates the input value and logs the event target.

~ _App.js_

```jsx .numberLines
function App() {
	const [value, setValue] = useState('');

	const eventHandler = (ev) => {
		setValue(ev.target.value);
		console.log(ev.target);
	};

	return (
		<>
			<input value={value} placeholder='Enter some text here' onChange={eventHandler} />
		</>
	);
}

export default App;
```

## State

> **State** - Data that changes throughout the life cycle of the app.
>
> We use **props** to share data between components, but how do we actually modify that data.
> **props** are _immutable_, so we can just change the value anywhere and expect React to update the UI.

For data that changes, React provides a **hook** called `useState()`.

A **hook** is a function that can be called in the top level of your component, to use different features of the framework.

`useState(default_value)` creates a stateful value and when it changes it will automatically re-render any components that depend on it.

It takes a default value as an argumant, and returns two values in an array.

It's common to destructure these values, with the _1st_ element being the actual value you want to use in the UI, and the _2nd_ value being a function you can use to render a different value.

```jsx .numberLines
const [count, setCount] = useState(0);
/* `count` = actual value you want to use in the UI */
/* `setCount` = a function that you can use to render a different value */
```

##### Example 1):

> A button that counts upward everytime you click the button

<iframe style="width: 100%;" scrolling="no" title="CodePen" src="https://codepen.io/parkercode98/embed/preview/zYjRLYY?default-tab=js%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
</iframe>


##### Example 2):

> Working with Arrays or Objects with useState.
> When you set a new value it will completely override the old one.

If you want to merge a new value into an array or object, its common to use the **spread syntax** to merge the old value into a new object.

<iframe style="width: 100%;" scrolling="no" title="CodePen" src="https://codepen.io/parkercode98/embed/preview/abGqjOv?default-tab=js%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
</iframe>

<br />

### Redux

<iframe style="width: 100%;" scrolling="no" title="CodePen" src="https://codepen.io/parkercode98/embed/preview/LYmQBNb?default-tab=js%2Cresult&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
</iframe>





## Lifecycle and Effects












<blob></blob>

