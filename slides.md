---
theme: default
class: text-center
highlighter: shiki
lineNumbers: true
info: |
  ## React Slide Deck

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
transition: slide-left
title: Intro to React
---
<div class='wrapper'>
<img src='https://media.giphy.com/media/eNAsjO55tPbgaor7ma/giphy.gif' alt='Animated react logo' class='image' />
</div>

# React!

A brief introduction.

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press space or right arrow for next page <carbon:arrow-right class="inline"/>
  </span>
</div>
<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/MollyJeanB/learn-react-slides" target="_blank" alt="GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<style>
.wrapper {
	display: flex;
	justify-content: center;
}

.image {
	width: 200px;
}
</style>

<!--
Welcome! Today we're going to talk about React. I have a short intro lesson for you, and then we'll dive right into some code.
If you touch any frontend code at EquipmentShare, there’s a good chance it’ll be written in React
I tend to get very excited and speak a little too quickly, so please let me know if you need me to slow down or repeat anything.

-->
---
layout: center
class: text-center
---
# What is React.js?

Tell me about your experience with React so far
---

# React is...

- 🧩 A open source JavaScript library built by Meta
- 📝 According to the [React docs](https://react.dev/), it is a “declarative, efficient, and flexible JavaScript library for building user interfaces." It lets you compose complex UIs from small and isolated pieces of code called 'components'
- 👩‍💻 One of the most popular ways to build modern web applications (over 9 million weekly downloads from npm!)
- ⚡️ Super fast, flexible, and scalable
- 🎂 10 years old as of May 2023
- 🥳 An absolute joy! 

<div class='wrapper'>
	<img src='https://media.giphy.com/media/9DtysFl2adFSEeiL47/giphy.gif' alt='Animated react logo' class='image' />
</div>

<style>
.wrapper {
	display: flex;
	justify-content: center;
}

.image {
	width: 350px;
}
</style>

<!--
- React components are often compared to building with legos-using many self-contained discrete parts to make up a whole. I think that maybe Matryoshka dolls are a better analogy, because components can be nested inside each other, and they can be reused in different places. But maybe the best visual analogy would be a set of Matryoshka dolls made out of legos.
- As probably the most popular way to build web applications these days, React is an incredibly wide-ranging library. There are many, many approaches to writing react code and about a zillion tools and compatible packages and libraries to explore
- That said, today’s lesson will be a pretty brief introduction to get you started writing and updating components. If you’ve already work with React, this may be a bit of a refresher for you

-->
---
---
# The Virtual DOM
React was developed to solve a problem: how to efficiently update the Document Object Model (DOM).

In React, for every DOM object, there is a corresponding “virtual DOM object.” A virtual DOM object is a representation of a DOM object, like a lightweight copy.

A virtual DOM object has the same properties as a real DOM object, but it lacks the real thing’s power to directly change what’s on the screen.

Manipulating the DOM is slow. Manipulating the virtual DOM is much faster because nothing gets drawn onscreen. Think of manipulating the virtual DOM as editing a blueprint, as opposed to moving rooms in an actual house[^1]

<img src='https://media.giphy.com/media/xT5LMNiPVoEQoc96XC/giphy.gif' alt='Animated react logo' class='image' />

[^1]: Source: this great [quick explainer from Code Academy](https://www.codecademy.com/article/react-virtual-dom).

<style>

.image {
	width: 200px;
}
</style>
---
---
# JSX

React uses a syntax extension called JSX that looks like a combination of HTML and JavaScript. 

```js
const h1 = <h1>Hello, interns!</h1>
```
It gets compiled into regular JavaScript in the browser
JSX elements are treated like regular old JavaScript expressions, which means they can be saved as a variable, stored in object or array, or passed to a function.

Just like HTML elements, JSX elements can have attributes, like this: 
```js
const h1 = <h1 id='intern-title'>Hello, interns!</h1>
```
A fun little gotcha with JSX is that all elements in a component must be within the same parent element. If they don't all naturally go within the same parent, you can use a fragment, which can be expressed as an empty tag, like this:
```js
<>
	<h1>Hello, friends!</h1>
	<p>We are child elements that need to be wrapped in a parent!</p>
</>
```
---

# Class Components versus Functional Components
A React component can be written as either a JavaScript class or a function. Functional components are more popular these days, since they can leverage newer feature like React hooks. However, you may encounter class components in older code.

Here's a class component:
```js {all|1|2|3|all}
export class WelcomeHeading extends React.Component {
   render() {
       return (
           <h1>Hello, friends!</h1>
       )}
}

```
And here's the same thing as a functional component:
```js {all|1|2|all}
export const WelcomeHeading = ( ) => {
   return (
       <h1>Hello, friends!</h1>
   )
}

```
---
---
# Consuming Components
Now here's how we'd consume the component from the previous slide. You can think of it like calling a function which then renders the component on the page

```js {all|1|3|4|7|all}
import { WelcomeHeading } from './some/example/file'

export const ConsumerWrapper = () => {
   return (
		<div>
			<h1>{`Here's a heading in the parent component!`}</h1>
			<WelcomeHeading />
		</div>
   )
}

```

---
---
# Props
To customize components and make them reusable across our app, we have props! 

Here's a class component that receives a title and an action as props:

```js {all|3}
export class Button extends React.Component {
   render() {
       const { title, action } = this.props;
       return (
           <button onClick={action}>
           { title }
       </button>
       )
   }
}

```

And the same as a functional component:

```js {all|1}
export const Button: React.FC = ( { title, action } ) => {
   return (
       <button onClick={() => action()}>
           { title }
       </button>
   )
}
```
---
---
# Passing Props
Passing props looks like adding attributes to an HTML element and you can think of them like parameters in a function.

Now here's how we'd pass the title and button props from a parent to the button component from the previous slide:

```js {all|5}
import { Button } from './some/example/file'

export const ConsumerWrapper = () => {
  return (
      <Button title={'Click me!'} action={() => console.log('Hello')} />
  )
}

```

A quick note on passing props: as you app gets more complicated, you may find yourself passing the same prop—an array of data, for example—from parent component to child to the child's child and so on. A better approach than this bucket brigade is something called React Context, which you can learn more about in the [React docs](https://react.dev/learn/passing-data-deeply-with-context).

---
---
# State
In addition to having things like data, strings, and functions passed down from parent components, components may need to control their state internally, like in this example from the React docs where the component keeps track of how many times the button has been clicked. 

In this example, we'll focus on a functional component example

```js {all|4|9}
import React, { useState } from 'react';

function Example() {
 const [count, setCount] = useState(0);

 return (
   <div>
     <p>You clicked {count} times</p>
     <button onClick={() => setCount(count + 1)}>
       Click me
     </button>
   </div>
 );
}

```

---
---
# Hooks
Hooks let you use different React features from your components. 

The component from the previous slide uses the useState hook, which lets you add React state to functional components. That's probably the hook you'll see most often, along with useEffect, which lets you perform side effects in function components. 

```js {all|13|4|5|7-12}
import { useEffect, useState } from 'react';
import { createConnection } from './chat.js';

function ChatRoom({ roomId }) {
  const [serverUrl, setServerUrl] = useState('https://localhost:1234');

  useEffect(() => {
    const connection = createConnection(serverUrl, roomId);
    connection.connect();
    return () => {
      connection.disconnect();
    };
  }, [serverUrl, roomId]);
  // ...
}
```

You can find a full list of hooks in the [React docs](https://react.dev/reference/react), and you can also write custom hooks!

---
---
# Custom hooks
These allow you to use React hooks outside of an individual component, which allows you to reuse logic across components. 

Here's an example of a custom hook that updates the height of a textarea when the value changes.

```ts
import { useEffect } from "react"

// Updates the height of a <textarea> when the value changes.
export const useAutoResizeTextArea = (
	textAreaRef: HTMLTextAreaElement | null,
	value: string
) => {
	useEffect(() => {
		if (textAreaRef) {
			// reset the height in initially to get the correct scrollHeight for the textarea
			textAreaRef.style.height = "24px"
			const scrollHeight = textAreaRef.scrollHeight

			textAreaRef.style.height = scrollHeight + "px"
		}
	}, [textAreaRef, value])
}
```
---
layout: center
class: text-center
---

# Now you try it!
Exercise time 🤸🏼‍♀️

Starter code: https://github.com/MollyJeanB/react-telly

Deployed demo: https://react-telly.vercel.app/

<div class='wrapper'>
	<img src='https://media.giphy.com/media/LmBsnpDCuturMhtLfw/giphy.gif' alt='Animated react logo' class='image' />
</div>

<style>
.wrapper {
	display: flex;
	justify-content: center;
}

.image {
	width: 250px;
}
</style>
---
layout: center
class: text-center
---

# Keep in touch!

[Portfolio + Contact Info](https://www.mollyjeanbennett.com/) · [GitHub](https://github.com/MollyJeanB) · [LinkedIn](https://www.linkedin.com/in/mollyjeanbennett/)

<div class='wrapper'>
	<img src='https://media.giphy.com/media/ia7kRlpGe3IFq/giphy.gif' alt='Animated react logo' class='image' />
</div>

<style>
.wrapper {
	display: flex;
	justify-content: center;
}

.image {
	width: 250px;
}
</style>