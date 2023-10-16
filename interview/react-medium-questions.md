1. **What is the purpose of the key prop in React lists, and why is it important?**
   - The key prop is used to uniquely identify elements in a list of components. It is essential for React's virtual DOM reconciliation process. When the order or structure of a list changes, React uses keys to efficiently update, add, or remove elements. Keys should be unique among siblings in a list.

2. **Explain the concept of "lifting state up" in React. When and why is it necessary?**
   - "Lifting state up" is a pattern in React where you move the state of a component higher in the component hierarchy to share it with other components. This is necessary when multiple components need access to the same data or when you want to maintain a single source of truth for shared state. It improves data consistency and reduces complexity.      

3. **What are controlled and uncontrolled components in React forms?**
   - Controlled components are React components where the form elements (e.g., input, textarea) get their values and changes controlled by React's state. Uncontrolled components, on the other hand, allow the DOM to handle the form element's state. In controlled components, you have full control over the form input, making it easier to validate and manipulate data.   

4. **What is Redux, and how does it relate to React?**
   - Redux is a state management library for JavaScript applications, often used with React. It provides a centralized store for application state and allows predictable and consistent data flow. React components can access the Redux store and dispatch actions to update it, making it easier to manage and share data across the application.   

5. **Explain the significance of React Router. How does it help with routing in a React  application?**
  - React Router is a library that provides client-side routing for single-page applications. It allows you to define routes and associated components, enabling navigation between different parts of your application without full page reloads. React Router helps in creating a more dynamic and responsive user experience.    

6. **What is the purpose of the componentDidMount lifecycle method in React, and when would you use it?**
   - `componentDidMount` is a lifecycle method that is called after a component has been added to the DOM. It is often used for data fetching, initialization, and setting up subscriptions. You would use it when you need to perform actions that should only occur after the component has been rendered and is in the DOM.

7. **What are React hooks, and how do they improve functional components in React?**
   - React hooks are functions that allow functional components to manage state, side effects, and more. Hooks like `useState` and `useEffect` provide functional components with the same capabilities as class components. They make it easier to reuse stateful logic and simplify functional component code.     

8. **Explain the concept of context in React. How can it be used for state management?**
   - Context is a feature in React that allows you to share data between components without passing props explicitly at every level of the component tree. It's often used for state management and global data sharing. By creating a context and provider, you can make data accessible to any component that subscribes to the context.  

9. **What is server-side rendering (SSR) in React, and what are its advantages?**
    - Server-side rendering is a technique that allows rendering React components on the server before sending the HTML to the client. The advantages of SSR include improved SEO, faster initial page loads, and a better user experience by delivering a fully-rendered page to the client, reducing the reliance on client-side rendering for content display.

10. **Explain the concept of lazy loading in React and how it can improve application performance.**
    - Lazy loading is a technique in React that defers the loading of certain components until they are actually needed. This can significantly improve application performance by reducing the initial bundle size and loading only the code necessary for the current page, leading to faster load times.
11. **Explain the differences between controlled and uncontrolled components in React forms.**
    - Controlled components are React components in which the form elements, such as input fields, are controlled by React state. Changes in the form elements are handled by React. Uncontrolled components allow the DOM to handle the form element's state, and React does not control their values. Controlled components provide more control over form data and allow for validation and manipulation.

12. **What is the purpose of React Router, and how does it help with routing in a React application?**
    - React Router is a library for handling client-side routing in single-page applications. It allows you to define routes and associate components with those routes. This enables navigation between different parts of the application without requiring full page reloads. React Router makes it possible to create a more dynamic and responsive user experience. 

13. **What is the purpose of the shouldComponentUpdate method in class components?**
    - The shouldComponentUpdate method is used to control when a component should re-render. By implementing this method and returning true or false based on certain conditions, you can optimize performance by preventing unnecessary re-renders when the component's props or state haven't changed. This can be useful for improving performance in certain scenarios.  

14. **What are arrow functions? How are they used?**
    - Arrow functions, also called ‘fat arrow‘ (=>), are brief syntax for writing the expression. These functions bind the context of the components because auto binding is not available by default in ES6. Arrow functions are useful if you are working with the higher-order functions.
```javascript
    Example
        //General way//
          render() {
          return(
              <MyInput onChange={this.handleChange.bind(this) } />
          );
          }

        //With Arrow Function//
          render() {
          return(
            <MyInput onChange={ (e) => this.handleOnChange(e) } />
          );
          }
```
15. **How to create a component in react js?**  
    - There are 3 ways to create a component in React:
    1)Using a depreciated variable function
    2)Using a Class
    3)Using a Stateless Functional Component
    1. Using a depreciated variable function
    In this, you need to declare a variable in your Javascript file/tag and use the React.createClass() function to create a component using this code.

    var MyComponent = React.createClass({
    render() {
        return <div>
        <h1>Hello World!</h1>
        <p>This is my first React Component.</p>
        </div>
    }
    })
    Now, use the div element to create a unique ID for the specific page and then link the above script onto the HTML page.
```javascript <div id=”react-component”></div>
```
    

    Use ReactDOM.render() function to take 2 arguments, the react component variable and the targeted HTML page.

    ReactDOM.render(<MyComponent />, document.getElementById('react-component'))

    2. *Using a Class*
    Javascript has lately started supporting classes. Any React developer can easily create a class using the class extends (Inherits). Following is the code

    3. Using a Stateless Functional Component
    It might sound a bit complex, but this basically means that a normal function will be used in place of a variable to return a react component.

    Create a const called MyComp and set it as equal to a () function. Use the arrow function, => to declare the logic of the function as follows:
````javascript
    const MyComponent = () => {
    return <div>
    <h1>Hello!</h1>
    <p>This is my first React Component.</p>
    </div>
    }
````
