---
layout: post
title:      "The React-Redux Circle of Life"
date:       2021-03-24 21:53:49 +0000
permalink:  the_react-redux_circle_of_life
---


React and Redux together make an undisputed pair for a web app combining reusable components and a global state manager.

Let's take a few moments to understand how this cycle works and how this created a wonderful flow for your web apps

When the app is started Redux is used at the top level. As the app is started Redux uses 
```createStore()``` this creates a global object that holds the state of the application. This global object can be accessed throughout the app as long as your component is hooked up with the ```connect()``` function.

As the state is updated then the UI or user interface is updated as well rendering the current data from the Redux Store. On this level when a user updates the state it then calls an Action creator that will return an Action to the reducer. Generally actions are objects made up of a type and payload.

When the action is passed to the reducer the type will determine which function is used to update the state. This is generally done with a switch statement. The reducer will return a new state which is then saved to the Redux store.

Now as previously stated when the Redux Store is updated this in turn updates the UI and starts the cycle over again. This creates an environment for your app to only update when needed and keep the app rendering the new state or data presented.
