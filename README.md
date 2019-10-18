# Hands on React

Do this hands on if you want to learn React basis.
To do it, you must have basic knowledge in javascript, html and css.

If you have any question, you may look at the [official React doc](https://en.reactjs.org/docs/getting-started.html).

You may use the basic code here to begin your app.

## The app

The app we're going to create is a Sudoku checker.

The 9x9 grid shall begin empty. The user will enter each number and we will check if each entry respects the rules of Sudoku.

Here are Sudoku's rules :

- all entries must be a number between 1 and 9
- The grid is divided in 9 3x3 grids
- A number cannot be present twice in a grid
- A number cannot be present twice in a row
- A number cannot be present twice in a column

When an error is detected, it will be shown to the user.

When the Sudoku is completed with no error, a success message will be shown.

## Instructions

React is a component based library. It helps you manage states updates of a part or all of your website.

Each component can take props in entry, has an inner state and renders html in output. It reacts to any change in props or state to update the output.

To begin, we will create the basic component of our Sudoku app, the input of our user.

### Input component

This component will only display an `<input type="number"></input>`, listen when it is modified and update its state accordingly.

Its state can be either `valid` or `invalid` (you may represent it with a boolean). When its state is incorrect, it adds a css class to the input to show the user it's a wrong value.

#### Code it

You can code a component in different styles, but the basic one is the class one.

Create a `.jsx` file (advice : create a `component` folder) :

```jsx
  import React from 'react'

  class YourComponent extends React.Component {
    constructor(props) {
      super(props)
      // You can define your state here
      this.state = {}
    }

    render() {
      return (
        // className is used to generate a css class
        <div className="container">
          {
            // To insert js in html, use {}
            // This will render the prop "name"
            this.props.name
          }
        </div>
      )
    }
  }

  export default YourComponent
```

To change the state of a component, you must use `setState()`

```javascript
  // In a method of your class
  this.setState({
    ...this.state,
    stateValue: newValue
  })
```

To use a method in the html part of the render, you must do :

```jsx
  (<div onClick={() => this.handleClick()}>Click me !</div>)
```

To use a component, you must import it and then use it like an html tag. You may pass props to it too.

```jsx
  import Component from './path/to/Component'
  ...

  render() {
    return (
      <div>
        <Component name="toto"></Component>
      </div>
    )
  }
```

#### Test it

In your tests, you can import the component and test its methods and construction directly. You can also find a dedicated [doc](https://fr.reactjs.org/docs/testing.html) on React official website.

### Grid component

This component will create the 9x9 grid and contain the logic for checking a line, a column or a 3x3 grid. To do that, we must change our Input component so that the Grid component will receive the value of the Input and manage it.

To communicate between components, Grid will pass to the Inputs a prop that is a js method. That prop will be called in the Input component when a change occurs. that method will change the Grid state and check if everything is valid.

```jsx
// Grid
  changeValue(value) {
    // setState
    // call check of column, line and grid
  }

  render() {
    return (
      <Input onChange={() => changeValue}></Input>
    )
  }

// Input
  handleChange(event) {
    // Checking value and setting state accordingly
    this.props.onChange(event.target.value)
  }

  render() {
    return (
      <input onChange={() => handleChange}></input>
    )
  }
```

When an Input is on an invalid line, column or grid, we want to set it to invalid state. To do that, we need to change the invalid data from a state one to a prop one.
