
#### 1.  What is React?
   React is a JavaScript library for building user interfaces.  It's an open-source, component-based library that's responsible for the view layer of an application. It allows developers to create reusable UI components and manage the state of those components efficiently.

#### 2. **What is JSX in React**
   - JSX stands for JavaScript XML. It is a syntax extension for JavaScript that allows you to write HTML-like code within your JavaScript code. React uses JSX to define the structure of its components.   
          
#### 3. **Explain the difference between React and React Native.**
   - React is a JavaScript library for building web applications. while React Native is a framework for building native mobile applications (iOS and Android) using React. React Native uses native components, while React focuses on web components.

#### 4. **What are React components**
   - React components are the building blocks of a React application. They are reusable UI elements that can be composed together to create complex user interfaces. Components can be either class-based or functional of the user interface.

#### 5. **What is the Virtual DOM in React**
   - The Virtual DOM is a lightweight in-memory representation of the actual DOM. React uses the Virtual DOM to improve performance by reducing the number of direct manipulations to the real DOM. When changes are made in a React component, they are first applied to the Virtual DOM, and then React calculates the most efficient way to update the real DOM.

#### 6. **Explain the concept of state in React**
   - State in React is a data structure that represents the dynamic data that can change over time. It is used to store and manage component-specific data. When the state of a component changes, React automatically re-renders the component to reflect those changes.

#### 7. **What is the difference between props and state in React?**
   - Props (short for properties) are used to pass data from a parent component to a child component. They are immutable and are set by the parent. State, on the other hand, is managed within a component and can change over time. It is used for the component's own data.

#### 8. **How can you handle events in React?**
   - In React, you can handle events by adding event handlers as props to JSX elements. For example, you can use `onClick` for handling click events and `onChange` for handling input changes.

#### 9. **Explain the purpose of the `key` prop in React lists.**
   - The `key` prop is used to uniquely identify elements in a list of components. It helps React optimize rendering when the list changes by ensuring that it can efficiently update, add, or remove elements without re-rendering the entire list.

## React Components ##

 10. **What is a React component lifecycle?**
    - React component lifecycle refers to the various phases a component goes through, from initialization to unmounting. The key lifecycle methods include `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`, which allow you to hook into different points in a component's lifecycle.

12. **Explain the difference between a functional component and a class component in React.**
    - Functional components are stateless and defined as JavaScript functions, while class components can hold state and have additional features like lifecycle methods.

11. **How do you create a functional component in React?**
    - To create a functional component, you define a JavaScript function that returns JSX. For example:
    ``react
        function MyFunctionalComponent() {
            return <div>Hello, World!</div>;
        }

12. **How do you create a class component in React?**
    - To create a class component, you define a JavaScript class that extends `React.Component` and includes a `render` method that returns JSX. For example:
    ``react
    class MyClassComponent extends React.Component {
    render() {
        return <div>Hello, World!</div>;
        }
    }

13. **What is the purpose of props in a React component?**
    - Props (short for properties) are used to pass data from a parent component to a child component. They allow components to be dynamic and customizable.
      
14. **What is the purpose of render() in React?**
    - It is compulsory for each React component to have a render(). If more than one element needs to be rendered, they must be grouped inside one tag such as <form>, <group>,<div>.           This function goes back to the single react element which is the presentation of native DOM Component. This function must return the same result every time it is invoked.

15. **What is the state in a React component**
    - State is a built-in object in React that represents the mutable data specific to a component. It can be used to store and manage data that can change over time.

16. **What is a higher-order component (HOC) in React?**
    - A higher-order component is a function that takes a component and returns a new component with additional props or behavior. It is a way to reuse component logic.

17. **How do you initialize and update the state of a React component?**
    - State is initialized in the constructor of a class component using `this.state`. It can be updated using `this.setState()` to trigger re-renders and reflect changes in the UI.

18. **What are Class Based Component?**
    - Class Based Component is the JavaScript Class. In these Components we extends the JavaScript predefined class into our component.

   Example:
        Import React,{Component} from ‘react’;

        class ABC extends Component {

        render(){

        return(

            <div>

            <h1>Hello World</h1>

        </div>

        );

        }}

        export default ABC;       

