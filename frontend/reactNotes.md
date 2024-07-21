# React Notes

## Component State

### When to uplift the state?

- To collect data from multiple children, or to have two child components communicate with each other, declare the shared state in their parent component instead. The parent component can pass that state back down to the children via props. This keeps the child components in sync with each other and with their parent.

### When a componnet re-renders?
- Scenario: A acomponent has useState 'squares & setSquares'. Calling the setSquares function lets React know the state of the component has changed. This will trigger a re-render of the components that use the squares state (Board) as well as its child components (the Square components that make up the board).

- The component along with its child components render when its state is updated, other components remain same.

### Props
- We can pass functions in props as well, functions such as the ones updating state of the component.

### Difference in func and func() in Props

Let's say we ahve function named handleClick. If we pass handleClick in prop, it means tis function i spassed down to the child component and will be called when there is a click from child component.  If we pass handleClick() (with brackets) in prop, we will call this function as soon as we try to pass this function in prop, which would re render the componnet again, resulting in calling this again when trying to pass it down the prop. It results in endless loop. So we don't place () with functions while passing those as props to child components. If we have to pass some value to function as params, we pass the whole function like below:
        
```<Square value={squares[3]} onSquareClick={() => handleClick(3)} /> ``` <br>

Instead of doing it like: <br>

```<Square value={squares[3]} onSquareClick={handleClick(3)} /> ``` <br>


## Thinking in React

### How to Build Project Static Structure

The most straightforward approach is to build a version that renders the UI from your data model without adding any interactivity… yet! It’s often easier to build the static version first and add interactivity later. Building a static version requires a lot of typing and no thinking, but adding interactivity requires a lot of thinking and not a lot of typing.

To build a static version of your app that renders your data model, you’ll want to build components that reuse other components and pass data using props. 
- Props are a way of passing data from parent to child.
- If you’re familiar with the concept of state, don’t use state at all to build this static version. 
- State is reserved only for interactivity, that is, data that changes over time. Since this is a static version of the app, you don’t need it.
- You can either build “top down” by starting with building the components higher up in the hierarchy or “bottom up” by working from components lower down. 
- In simpler examples, it’s usually easier to go top-down, and on larger projects, it’s easier to go bottom-up.

### Identifying State!

- Does it remain unchanged over time? If so, it isn’t state.
- Is it passed in from a parent via props? If so, it isn’t state.
- Can you compute it based on existing state or props in your component? If so, it definitely isn’t state!