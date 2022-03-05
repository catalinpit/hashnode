## React Class Components to Functional Components With Hooks

Refactoring React class components to functional components with Hooks is quite a journey. Recently, I had to refactor an entire React application so I want to share my process and learnings.

## Introduction to React Hooks

Functional components use Hooks, so it makes sense to introduce them before going further.

React Hooks were added in React 16.8 and they allow you to use state and other React features without using a class. Previously, you had to use a class if your components needed to use state.

The React documentation describes Hooks as follows:

> "Hooks are functions that let you “hook into” React state and lifecycle features from function components." - [React Docs](https://reactjs.org/docs/hooks-overview.html#but-what-is-a-hook)

By default, React comes with Hooks such as `useState` and `useEffect`, but you can also create custom ones. For example, you can create a custom hook to access the previous value of props since there is no default hook for this.

The `useState` hook enables you to add state to your functional components. The code snippet below shows an example:

```javascript
function App() {
  const [counter, setCounter] = useState(0);

  return (
    <div>
      <h1>Counter</h1>
      <p>current value: {counter}</p>
    </div>
  );
}
```

The hook takes one argument which represents the initial state. In this case, the "counter" variable has the initial state of "0". It also returns a pair of values:
1. the current state - you can access the current state by using the `counter` variable
2. a function to update the state - you can update the state by calling the `setCounter` method and passing an argument that represents the new state

The other hook - `useEffect` - allows you to perform side effects. The `useEffect` hook replaces the lifecycle methods from the class components.

> "You can think of useEffect Hook as componentDidMount, componentDidUpdate, and componentWillUnmount combined." - [React Docs](https://reactjs.org/docs/hooks-overview.html#but-what-is-a-hook)

Let's continue with the same "counter" example and log to the console when the state gets updated.

```javascript
function App() {
  const [counter, setCounter] = useState(0);

  useEffect(() => {
    console.log("The new counter value is ", counter);
  }, [counter]);

  return (
    <div>
      <h1>Counter</h1>
      <p>current value: {counter}</p>
      <button onClick={() => setCounter(counter + 1)}>Click</button>
    </div>
  );
}
```

The above code is the equivalent of using `componentDidMount` in class components.

Now that you are up-to-date with React Hooks let's discuss why you might want to use functional components with Hooks.

## Why Functional Components with Hooks?

One of the benefits is that functional components are less verbose. A functional component requires less boilerplate code, making it more concise and easier to understand.

Looking at the two examples above, you can already see how neat a functional component looks. If you want to do an exercise, convert them into class components to see the difference.

Another benefit is getting rid of the `this` keyword and all the confusion it can bring. In functional components, you do not have the `this` keyword. You also do not have method bindings anymore.

Lastly, with class components, it's difficult to re-use the stateful logic between components. Functional components with Hooks aim to make it easier to re-use stateful logic without changing the component hierarchy.

If these reasons did not convince you to use functional components with Hooks, I encourage you to read the [motivation](https://reactjs.org/docs/hooks-intro.html#motivation) behind them.

## Class Components to Functional Components

Let's look at the main differences between class and functional components and how to convert them.

### 1. Syntax

One noticeable difference between them is the syntax. A class component extends the `React` component and comes with the `render` method.

```javascript
class Home extends React.Component {
    render() {
        return (
            <h1>Hello!</h1>
        )
    }
}
```

On the other hand, a functional component is a JavaScript function.

```javascript
function Home() {
    return (
        <h1>Hello!</h1>
    )
}
```

As you might observe, the functional component is less verbose. A functional component does not have:
* constructor
* `this` keyword
* event handler bindings
* `render` method

The difference in syntax is more striking once you refactor a complex class component.

### 2. Props

In a functional component, you pass the `props` as an argument to the function.

```javascript
function Home(props) {
    return (
        <h1>Hello, {props.name}!</h1>
    )
}
```

Also, it does not have the `this` keyword, so the way you access `prop` is simpler too.

### 3. State

How a functional component handles state is very different from how a class component does it.

The code snippet below illustrates how class components handle state.

```javascript
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      vehicleId: 0
    };
  }

  render() {
    return (
      <div>
        <h1>Update Vehicle ID</h1>
        <p>vehicleId: {this.state.vehicleId}</p>
        <button onClick={() => this.setState({ vehicleId: this.state.vehicleId + 1 })}>Click</button>
      </div>
    );
  }
}
```

In class components, you need to implement a `constructor` and call `super(props)` if you want to initialize state. Not doing it can lead to bugs such as your state variables being "undefined".

When it comes to accessing the variables, you access them by using the `this` keyword. Lastly, you set state by calling the `setState` method.

Now, let's look at how you handle state in functional components.

```javascript
function App() {
  const [vehicleId, setVehicleId] = useState(0);

  return (
    <div>
      <h1>Update Vehicle ID</h1>
      <p>vehicleId: {vehicleId}</p>
      <button onClick={() => setVehicleId(vehicleId + 1)}>Click</button>
    </div>
  );
}
```

If you worked with React before, you might know that handling state in functional components was not possible. That changed with the introduction of Hooks.

The `useState` hook is equivalent to `this.state` from class components, enabling us to write stateful functional components.

`useState` takes only one argument, which represents the initial state. We set the initial state for `vehicleId` to "1" in the above example. It also returns a pair of values:
* the current state - "vehicleId" in this case
* a function that allows you to update the state - "setVehicleId" in this case

The verbosity resulting from building the constructor is replaced by one line.

### 4. Lifecycle Methods

In functional components, the `useEffect` hook replaces the lifecycle methods. Let's take each lifecycle method separately and convert them to "useEffect".

#### componentDidMount()

The lifecycle method - `componentDidMount()` - is invoked after a component is mounted. 

Let's use the same example with the vehicle from above. For illustrative purposes, let's say we want to set the vehicle id to "1" when the component gets mounted. You would do it as follows in a class component:

```
componentDidMount() {
    this.setState({ vehicleId: 1 });
}
```

When it comes to functional components, you could achieve the same thing with `useEffect` as follows:

```
useEffect(() => {
    setVehicleId((vehicleId) => vehicleId + 1);
}, []);
```

Notice that we pass an empty array to the hook. That means it only runs once - when the component is mounted.

**The purpose of the second argument**

The `useEffect` hook accepts an array of values as a second argument and it is optional.

The reason is that `useEffect` runs after every complete render, which might not be desirable in all cases. So, you can pass an array of values that tells the `useEffect` hook - "Hey, only run when one of these values changes".

In the above case, the dependency array is empty so it only runs once.

#### componentDidUpdate()

Continuing with the vehicle example, let's say we want to log the vehicle id each time it is updated. In a class component, you can do it as follows:

```
componentDidUpdate() {
    console.log("Vehicle updated", this.state.vehicleId);
}
```

Each time the vehicle id changes, the application logs the new id in the console. You can achieve the same thing with Hooks as follows:

```
useEffect(() => {
    console.log("Vehicle updated", vehicleId);
});
```

Notice that there is no second argument. The reason is that the `useEffect` is invoked each time the component renders.

#### componentWillUnmount()

The lifecycle method `componentWillUnmount()` is executed when the component gets unmounted from the DOM and destroyed. The method is used when cleanup, such as removing event listeners or stopping intervals, is required.

Let's assume you want to set a timer when the component mounts and remove it when it unmounts. In class components, you would do it as follows:

```
componentDidMount() {
    // set up the timer
}

componentWillUnmount() {
    clearInterval(this.state.timer);
}
```

You can achieve the same behavior with the `useEffect` hook this way:

```
useEffect(() => {
    // set up the timer

    return () => {
        clearInterval(this.state.timer)
    }
}, []);
```

As you might observe, we return a function from the hook. The function allows us to perform a cleanup after the effect runs. Whenever you need to perform a cleanup, return a function from the hook.

Also, the empty array (`[]`) tells the hook to run only when the component is mounted and unmounted.

## Summary

In this article, you learnt about Hooks and why you might want to use them in your React applications. After that, you saw how to convert your class components to functional components.
