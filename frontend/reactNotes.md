# React Notes

## Component State

### When to uplift the state?

- To collect data from multiple children, or to have two child components communicate with each other, declare the shared state in their parent component instead. The parent component can pass that state back down to the children via props. This keeps the child components in sync with each other and with their parent.

### When a componnet re-renders?
- Scenario: A acomponent has useState 'squares & setSquares'. Calling the setSquares function lets React know the state of the component has changed. This will trigger a re-render of the components that use the squares state (Board) as well as its child components (the Square components that make up the board).

- The component along with its child components render when its state is updated, other components remain same.

### Props
- We can pass functions in props as well, functions such as the ones updating state of the component.