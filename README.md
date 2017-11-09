# React Handling Events and Forms

## Learning Objectives

- Describe the concept and syntax of React components
- Describe the concept and syntax of State and Lifecycle in React
- Describe and implement the process of handling events in React
- Use conditional rendering to respond to various states
- Use `map` to produce a list of React elements and provide `key` props for efficiency
- Make a form of controlled components

![Doc Dive](https://media.giphy.com/media/3orifhJLiLIDxryOgo/giphy.gif)

Today we will be doing a series of doc dives and adding relevant features to our [Fictional Restaurant Roulette App](https://git.generalassemb.ly/wdi-nyc-thundercats/LAB_U03_D03_Fictional-Restaurant-Roulette).
We will start from where the lab left off. From the lab repo:

```
$ git checkout -b in-class stage-five
```

## Components and Props

### [Doc Dive](https://reactjs.org/docs/components-and-props.html)

- How are components like functions?
- What are the two ways we can define a component?
- What is the syntax for using components in JSX? What case do we use in our component names?
- What is meant by [composing components](https://reactjs.org/docs/components-and-props.html#composing-components)?
- Why do we want to extract components when possible?
- What is meant by [props are read only](https://reactjs.org/docs/components-and-props.html#props-are-read-only)?

### Exercise

We will be [pair programming](https://en.wikipedia.org/wiki/Pair_programming) on today's exercises.
When pair programming, we want to work in a driver - navigator arangement where the person at the keyboard doesn't need to be thinking ahead but simply about the current step of the implimentation.
The navigator meanwhile thinks about the big picture approach letting the driver worry about the technical details of the implementation.
We will switch drivers and navigators at the next exercise.

Add a component to the React app called `RestaurantForm`.
Define your componets as functions until you need a feature only available to classes.
The `RestaurantForm` should be made of two components, one to chose whether to create a new restaurant or to edit an existing restaurant (the `RestaurantSelector`) and a form with fields for editing a restaurants attributes (the `RestuarantEditor`).

The component `RestaurantSelector` should be a `select` element with a list of `options`.
We're eventually going to use the restaurant list with this but for now just hard code an option or two in.

Give `RestaurantSelect` a prop `restaurants` and make sure it works by hardcoding a value and logging it before rendering. But wait to use the list to create the options.

Give `RestaurantForm` input fields for name, description, media, category, image, source, and media category, and a submit button.

If you have extra time, create a `RestaurantForm.css` file and style the RestaurantForm.

## State and Lifecycle

### [Doc Dive](https://reactjs.org/docs/state-and-lifecycle.html)

- How does state differ from props? What kind of components do we need to use if we want state?
- How do you convert a component defined by a function to a component defined by a class?
- Where do we intialize a component's state? What else do we do here?
- How do we read from state?
- What is the lifecycle method that we use to set up a component? What is the lifecycle method we use to clean up after a component?
- How do we update a component's state?
- What are the ["three things you should know about `setState()`"](https://reactjs.org/docs/state-and-lifecycle.html#using-state-correctly)
- What does "mergining is shallow" mean?
- How do we pass state down to child components?

### Exercise

Change `RestaurantForm` to a component and initialize its state as `{selectedRestaurant: {}}`.
Write a method `selectRestaurantById` that will update the `selectedRestaurant` based on an id passed to the method. This method should update `selectedRestaurant` to be the restaurant object from the restraunts list, not just the id. If the method gets called with no argument, it should set selectedRestaurant to an empty object.

You can add these two elements to your `RestaurantForm` to test `selectRestaurantById`:

```
<button onClick={() => this.selectRestaurantById(1)} />
<p>{this.state.selectedRestaurant.name}</p>
```

Pass the selected restaurant to the `RestaurantEditor` as a prop.

## Handling Events

### [Doc Dive](https://reactjs.org/docs/handling-events.html)

- What are the syntactic differences between DOM event handling and React event handling?
- What is a synthetic event (high level definition)? Where do we see synthetic events?
- Why do we need to bind `this` on methods that will be event handlers and where do we do it?
- What are two alternatives to binding `this`?
- How do we pass extra arguments to an event handler?

### Exercise

Pass `selectRestaurantById` to `RestaurantSelector` as a prop. Add an `onChange` event handler to the select element of the `RestaurantSelector` that calls `selectRestaurantById`. For now pass it a hard coded value (something different than 1). You want to give each `option` of the select a `value` property. When the `onChange` handler is called, you can find the value selected with `e.target.value`

## Conditional Rendering

### [Doc Dive](https://reactjs.org/docs/conditional-rendering.html)

- What does it mean to conditionally render an element?
- What mechanisms are available to us in JavaScript that allow us to conditionally render?
- How do [element variables](https://reactjs.org/docs/conditional-rendering.html) let us render only part of a component conditionally?
- How are the logical and (`&&`) and the ternary/if-else operator used to conditionally render?
- What value should we render if we want a component not to render itself?

### Exercise

Add a conditional header and button to the `RestaurantEditor`. If the `selectedRestaurant` has an `id` property, the heading should read `Editing Restaurant` and the button should read `Save Changes`. If the `selectedRestaurant` doesn't have an `id`, the title should be `New Restaurant` and the button should be `Create`. Set the value on each of the input fields to come from `selectedRestaurant` as well.

## Lists and Keys

### [Doc Dive](https://reactjs.org/docs/lists-and-keys.html)

- What method do we use to apply a transformation to each element of an array and return a new array of the results of the transformation?
- What is the purpose of the `key` property?
- If we extract an component which is being created in a mapping, where does the key need to go?

### Exercise

Update the `RestaurantSelector`'s options so they are produced from the `restraunts` prop. Make sure they each have a key.
Add an option with a value of `null` for creating a new restaurant.


## Forms

### [Doc Dive](https://reactjs.org/docs/forms.html)

- What does "form elements naturally keep some internal state" mean?
- What is a "controlled component"? Why does this make it simple to validate or modify user input?
- What is different about React's `textarea` element than an HTML textarea?
- How can giving inputs a `name` prop help create a generic input change handler?
- BONUS: what is an uncontrolled component? How does this violate React's preference for declarative programming over impartive programming?

### Exercise

Define a gneric input change handler and make the form a controlled component.
Add an event handler for submitting the form the logs the form's inputs from the `App` component.
Depending on if the form sumbission is an edit or a create, PUT or POST to the API and get an updated list of restaurants.
