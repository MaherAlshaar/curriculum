---
author: catalin
type: normal
category: how to
links:
  - >-
    [Destructuring
    assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment){website}
  - >-
    [Destructuring objects as function
    parameters](https://simonsmith.io/destructuring-objects-as-function-parameters-in-es6/){website}
parent: jsx-spread-attributes
---

# Destructuring arguments


---

## Content

The **destructuring assignment** syntax, introduced in `ES6`, is used to extract data from either *arrays* or *objects* in distinct variables.

Basic assignment:

```jsx
const obj = {x: 13, y: 42};
const {x, y} = obj;

console.log(x); //13
console.log(y); //42
```

Using this, you can easily extract `props` from a **function component**:

```jsx
function Display({text}) {
  return <p>{text}</p>;
}
// is equivalent to:
function Display(props) {
  return <p>{props.text}</p>;
}
```

Additionally, you can use the **JSX spread attributes** to forward **DOM** `props` to your component:

```jsx
function Display({text, ...props}) {
  return <p {...props}>{text}</p>;
}
```


---

## Practice

Complete the following function component such that:

- `text` prop is displayed within a `<h1>`
- all other `props` properties are used as **DOM** attributes for the `<h1>` element

```jsx
function Enki({text, ???}) {
  return <h1 {...props}>???</h1>;
}
```

- `...props`
- `{text}`
- `props`
- `{props}`
- `text`
- `this.props.text`
- `props.text`


---

## Revision

Complete the following function component such that:

- `age` prop is displayed within a `<h1>`
- all other `props` properties are used as **DOM** attributes for the `<h1>` element

```jsx
??? Enki({age, ???}) {
  return <h1 {...props}>???</h1>;
}
```

- `function`
- `...props`
- `{age}`
- `props`
- `{props}`
- `text`
- `this.props.text`
- `props.text`
