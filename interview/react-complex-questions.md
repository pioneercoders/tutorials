
1. **Explain the concept of conditional rendering in React and provide an example.**
    - Conditional rendering in React involves showing or hiding components or elements based on specific conditions. Here's an example:
```javascript
    function Greeting(props) {
    if (props.isLoggedIn) {
    return <h1>Welcome back!</h1>;
    }
    return <h1>Please sign up or log in.</h1>;
    }
```

1. **How do you handle events in React, and what is event delegation?**
   - In React, you can handle events by defining event handlers as functions and attaching them to JSX elements. Event delegation is a technique in which a single event handler is placed on a common ancestor of multiple elements, allowing you to capture events from child elements efficiently.    

2. **What are controlled and uncontrolled components?**
 - A Controlled Component is one that takes the current value through the props and notifies of any changes through callbacks such as onChange.
```javascript
    *Example:*
    <input type="text" value={value} onChange={handleChange} />
```
    An uncontrolled component is one storing its own state internally, and you can query the DOM via a ref to find its current value as and when needed. Uncontrolled components are a bit closer to traditional HTML.
```javascript
    *Example*:
    <input type="text" defaultValue="foo" ref={inputRef} /> 
```

4. **How to redirect to another page in react js?**
  - The best way to redirect a page in React.js depends on what is your use case. Let us get a bit in detail:

    If you want to protect your route from unauthorized access, use the component
```javascript
    *Example*:
        import React from 'react'
        import { Redirect } from 'react-router-dom'
        const ProtectedComponent = () => {
        if (authFails)
        return <Redirect to='/login' />
        }
        return <div> My Protected Component </div>
        }
```
5. **How to call one component from another component in reactjs?**
    - To render a component with another component in Reactjs, let us take an example:

Let us suppose there are 2 components as follows:

```javascript
    *Example*
            Component 1

            class Header extends React.Component{
                constructor(){
                    super();
                }
                checkClick(e, notyId){
                alert(notyId);
                }
            }
            export default Header;

    **Component 2**
        class PopupOver extends React.Component{
            constructor(){
                super();        
            }
            render(){
                return (
                    <div className="displayinline col-md-12 ">
                        Hello
                    </div>
                );
            }
        }
        export default PopupOver;

        *Now to call the Component 1 in Component 2, use this code:*

        import React from 'react';

        class Header extends React.Component {
        constructor() {
            super();
        }
        checkClick(e, notyId) {
            alert(notyId);
        }
        render() {
            return (
                <PopupOver func ={this.checkClick } />
            )
        }
        };

        class PopupOver extends React.Component {
        constructor(props) {
            super(props);
            this.props.func(this, 1234);
        }
        render() {
            return (
                <div className="displayinline col-md-12 ">
                    Hello
                </div>
            );
        }
        }
        export default Header;
```

6. **Question 3: How do you handle form submission in React?**
    - Form submission in React can be handled by attaching an event handler to the form's onSubmit event. In the event handler, you can prevent the default form submission behavior, access form field values from the component's state, and send the data to a server or perform any necessary actions.

7. **What is the purpose of the event.preventDefault() method when handling form submissions in React?**
   -  The `event.preventDefault()` method is used to prevent the default browser behavior associated with form submissions, such as a full page reload. By calling this method, you can control how the form data is submitted and processed using JavaScript without the default behavior interfering.

8. **How do you validate form input in React?**
     - Form input validation in React is typically done by adding validation logic to the form's event handler. You can check the values of input fields against specific criteria, display error messages, and prevent form submission until all validation conditions are met.

9. **What is formik, and how does it simplify form handling in React applications?**
    - Formik is a popular library for managing forms in React. It simplifies form handling by providing utilities for form validation, error handling, submission, and keeping track of form state. It streamlines the process of building complex forms and reduces the amount of boilerplate code required.

10. **How can you handle form input from multiple related form elements in React, such as radio buttons or checkboxes?**
    - In React, you can handle related form elements by giving them the same name attribute and storing their values in an array in the component's state. This allows you to manage multiple selections or options effectively.
    
11. **What is the role of the defaultValue and value attributes in React form elements, and how are they used?**
    - The defaultValue attribute is used to set the initial value of a form element, while the value attribute is used to bind the element's value to the component's state. In controlled components, you typically use the value attribute to maintain a two-way binding between the element and the component's state.

12. **Explain the concept of context and the useContext hook in React. How can you use context to pass data between components?
    - Context is a feature in React that allows data to be shared between components without having to pass props explicitly through the component tree. It consists of a `Provider` that wraps a set of components and a `Consumer` or the `useContext` hook for accessing the data. You can create a context, provide data using the `value` prop of the `Provider`, and then consume that data in any child component that subscribes to the context. This is particularly useful for global state management or sharing data that is used by multiple components. 

13. **What is Redux, and how does it work with React? Can you explain the main principles of Redux and the components involved?**
    - Redux is a state management library for JavaScript applications, often used with React. The core principles of Redux are:
    *Single source of truth*: Application state is stored in a single, centralized store.
    *State is read-only*: You cannot modify the state directly; you dispatch actions.
    Changes are made with pure functions: Reducers specify how the state changes in response to actions.
    The key components in Redux are the store (which holds the application state), actions (describing what happened), and reducers (specifying how state changes in response to actions). React components can connect to the Redux store using the `connect` higher-order component or hooks like `useSelector` and `useDispatch`. 

14. **How do you optimize performance in React applications? Provide some techniques and best practices for improving rendering performance.**
    - Performance optimization in React can be achieved through various techniques and best practices, including:

    Memoization: Use tools like `React.memo` and `useMemo` to prevent unnecessary re-renders.
    Virtualization: Implement virtualized lists or grids to reduce the number of rendered items.
    Code splitting: Split your application into smaller chunks for lazy loading.
    Minimize re-renders: Carefully manage state updates and ensure that components only re-render when necessary.
    Avoid unnecessary prop drilling: Use context or state management solutions to share data without passing it through many components. 

15. **Explain the use of React hooks like useEffect and useState in functional components. Provide an example of how you would manage side effects with useEffect.**
    - React hooks like useEffect and useState allow functional components to manage side effects and state.

   ```javascript
        import React, { useState, useEffect } from 'react';

        function ExampleComponent() {
        const [count, setCount] = useState(0);

        useEffect(() => {
            document.title = `Count: ${count}`;
        }, [count]);

        return (
            <div>
            <p>Count: {count}</p>
            <button onClick={() => setCount(count + 1)}>Increment</button>
            </div>
        );
        }
   ```

16. **Explain the concept of higher-order components (HOCs) in React. Provide an example of how you would create and use an HOC.**
    - Higher-order components are functions that take a component and return a new component with additional props or behavior. They are often used for code reuse and abstraction. Here's an example of creating and using an HOC:
      
   ```javascript
    import React from 'react';

    function withLogger(WrappedComponent) {
    return function WithLogger(props) {
        console.log('Logging props:', props);
        return <WrappedComponent {...props} />;
    };
    }

    function MyComponent(props) {
    return <div>My Component</div>;
    }

    const ComponentWithLogger = withLogger(MyComponent);

   ```
