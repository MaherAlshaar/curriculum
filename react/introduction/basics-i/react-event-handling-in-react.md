---
author: catalin
type: normal
category: must-know
links:
  - >-
    [Handling
    events](https://facebook.github.io/react/docs/handling-events.html){website}
parent: forms-in-react
---

# Event handling in React


---

## Content

Adding **event handlers** in **React** is done by providing a listener to the element when initially `render`ed (and **not** by calling `addEventListener` like with regular DOM):

```jsx
class Click extends React.Component {
  render() {
    return (
      <button onClick={this.myListener}>
        Click
      </button>
    );
  }
}
```

A common practice when using **ES6 classes** is to have event listeners as separate methods in the class:

```jsx
// within Click component:
myListener(e) {
  console.log('button clicked');
  // 'button clicked'
  console.log(this.props.test); 
  // raises an error
}
```

Above, `e` is the **synthetic event**[1] passed when clicking the button.

To make the second `console.log` not throw an error, the `this` context of the `myListener` method must be explicitly bound to the `Click` class. 

The reason is that `this` in JavaScript depends on how a function is called, not where it is defined. 

If we call a function as a method on an object, i.e. `person.say()`, `this` will point to that object. 

If we call a function as a standalone function, i.e. `say()`, `this` will be `undefined`. 

Since we're passing `myListener` into a `button` as the `onClick` function, the `button` will internally call it as a regular function, i.e. `onClick()`, making the `this` be `undefined` and causing an error. By binding `this` to always point to our class instance, we can avoid this problem.

```jsx
class Click extends React.Component {
  constructor(props) {
    super(props);
    this.myListener =
      this.myListener.bind(this);
  }
  // ...
}
```

Another approach is to `bind` the function directly:

```jsx
render() {
  return (
    <button onClick={
      this.myListener.bind(this)}>
      Click
    </button>
  );
}
```

Although possible, it is advised against `bind`ing functions inside `render()` as it might cause excessive re-rendering (because React will re-render a component anytime it's `props` change and binding a function in `render` always creates a new function).

A similar effect can be achieved using either the **property initializer syntax**[2] or an **arrow function**[3] in the callback.


---

## Practice

Complete the `constructor` of the following **React Component** so that you can use `this` keyword in `myHandler()`:

```jsx
class Practice extends React.Component {
  constructor(props) {
    super(props)
    this.??? =
     ???.???(???)
  }
  myHandler() {
    console.log('practice');
  }
  // render()...
}
```

- `myHandler`
- `this.myHandler`
- `bind`
- `this`
- `myHandler()`
- `this.myHandler()`
- `bind()`
- `bind(this)`


---

## Revision

Add `clickCallback` as an event handler for the defined `<button>` in the following component:

```jsx
class Click extends React.Component {
  clickCallback() {
    console.log('clicked');
  }
  render() {
    return (
      <button ???={???}>
        Click
      </button>
    );
  }
}

```

- `onClick`
- `this.clickCallback`
- `clickCallback`
- `onMousePressed`
- `onclicked`
- `onclick`
- `this.clickCallback()`


---

## Footnotes

[1:synthetic events]
The `SyntheticEvent` is a cross-browser wrapper used by **React** whose instances are passed to event handling function.
It has exactly the same interface as the browser's native `event`.

[2:property initializer syntax]
This is an **experimental** *Stage 2* feature which is already set up when creating an app with `create-react-app`.

Note that there is no guarantee this will be adopted as a standard.

To use it the following `Babel` plugin must be installed:

```plain-text
npm install --save-dev
 babel-plugin-transform-class-properties
```

Then you can define the handler function which will be automatically `bind`ed like:

```jsx
myListener = (e) => {
  console.log('button clicked');
  console.log(this.props.test);
}
```

[3:arrow function]
Using the **arrow function** approach it will create a different *callback* every time `Click` component is `render`ed.
This is fine except in the case when the handler is passed as a `prop` to lower `component`s as they might do extra re-rendering.

Keep in mind this is considered a **bad practice**:

```jsx
// ...
return (
  <button onClick={(e) =>
      this.myListener(e)}>
    Click
  </button>
);
```
