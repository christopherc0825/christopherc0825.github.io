---
layout: post
title:      "Reacting to new React"
date:       2021-03-09 22:43:47 +0000
permalink:  reacting_to_new_react
---


In this post we will cover using newer React conventions that were not done justice by the lesson plans since they were not around when the lessons were written, which is a normal thing when developing apps as languages and frameworks are always evolving.

The lesson plan for Flatirons React section may mention functional components, however the majority of labs and codealongs are using class syntax.

```
import React, { Component } from 'react'

export default class App extends Component {
   render() {
	    return (
			   <div>
				    <h1>My App</h1>
				</div>
			)
		}
}
```

While this may be nice and makes writing javascript similar to other OOP languages. This approach seems very clunky and unnecessary for smaller components that do not require much logic. The above code snippet can be written like so

```
export default function App(props) {
  return (
	   <div>
				    <h1>My App</h1>
		  </div>
	)
}
```

or even with ES6 arrow functions which will help with context issues if they arise

```
const App = props => {
   return (
	    <div>
				    <h1>My App</h1>
		  </div>
	 )
}
```

Now this looks quite better and seems easier to read and understand what is going on.

You may be asking what about lifecycle methods that may be used when mounting, unmounting or updating components? Easy. React implemented special methods called React hooks which work just like the lifecycle methods. Also with JavaScript there is no issue writing functions inside of functions.

```
import React, { useEffect } from 'react'

const SampleContainer = props => {
   useEffect(() => {
	    //you can think of useEffect Hook as componentDidMount, componentDidUpdate, and
			//componentWillUnmount combined
			//this is used for anything that will make side effects such as fetching data or starting 
			//subscriptions
			fetchData()
	 }
	 
	 const fetchData = () => {
	    //Write the fetch statement
	 }
	 
	 return (
	    //JSX
	 )
}
```

This makes the code much cleaner than multiple functions running in a class as you can use (for most instances) one hook instead of multiple lifecycle methods.

While class syntax is still accepted the ease of functional components makes for quick developement of the main requirements to give you more time to refactor and optimize your codebase.

Additionally, it is always a good thing to learn new concepts and technologies to further help with easy and functional code.
