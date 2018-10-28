# Vue Overview


# Purpose

The purpose of this is to explain vue in simple and easy to understand terms.
Some objective we will cover are:

-   Why Vue.js is in many cases the better tool for for the job.
-   Quickly creating a project using the vue-cli.
-   Creating new components
-   Passing props from one component to another
-   Using Vue directives
-   Using Vue Events
-   Using Vue watchers

We may lightly and indirectly touch on:

-   Webpack
-   Bootstrap
-   ES6


## Requirements

-   Node v8.12+
-   NPM v6.4.1+

## Necessary Skills

-   Basic concept of front end frameworks
-   Javascript
-   Basic knowledge of ES^

## What is Vue?

Vue is a fast, lightweight, front-end Javascript based framework.

Every Vue app is an instance of of the ViewModel.  In plain english it is an
object that syncs that data with what we see in the DOM. Doing this, like many
other framework allows for a faster web experience.

Vue is unique in that is performs better than many other frameworks including
React and angular. [Metrics](https://stefankrause.net/js-frameworks-benchmark8/table.html)

It does not require a domain speific language, such as JSX.

HTML rendered in templates makes for easy conversion of large scale apps.

Assurances to be non-breaking. [Angular backwards compadiblity](https://www.codementor.io/codementorteam/migrating-from-angular-1-x-to-angular-2-upgrade-strategies-a3fgzrhxo)


# Getting Started

First we need the handy vue-cli tool which will quickly get us a full vue 3 app.

Let's install this with the command

```bash
npm install -g @vue/cli
```

Now that we've installed our command line tool let's scaffold our first Vue app.

```bash
vue create my-app
```

For now we don't need to worry about any config options and can just click enter
and accept the defaults.

Now let's take a look at what got scaffolded and run `npm run serve` to take
a look at our app.

## Clear and setup

First we're going to remove some of this starter code. So clear out everything
from `HelloWorld.vue`, the CSS inside `App.vue`, as well as everything inside
the `<div>` tags.

For now We'll also seed some initial in our main `App.vue` component like so:

```js
data(){
    return {
      todos:[{
      "id": 1,
      "title": "walk dog",
      "completed": false
      },
      {
      "id": 2,
      "title": "clean room",
      "completed": false
      },
      {
      "id": 3,
      "title": "get gas",
      "completed": false
      }]
    }
  }
```


## Render Child Component

Vue-cli already created a parent component for us let's render it and pass in
some data.

Since our component is imported as `HelloWorld` we can render it inside the
`<template>` tag as `<HelloWorld/>`.

To pass the `todos` we greated to the component we can use the vue syntax:

```vue
<HelloWorld :todos:="todos" />
```

The above says "pass in the data todos [the right side] can call it todos in the
child template [the left side]".

*Think: data down, actions up*

Now if we add a skeleton to our child component `HelloWorld.vue` we can we that
we have rendered it.

## Props: Rendering todos

The todos we created are being passed to the child component but yet recieved.
To do this we use `props`.  Along with passing the data to the child from
within the parent we also have to tell the child component to accept the data.

In our child component we will define a props array in our export object:

```js
props: ['todos'],
```

Now in the `<template>` tag we can use `{{todos}}` to render our pass in todos.

You may recognize the handlebars syntax `{{ }}`. Another advanage of vue is
that it takes the best part other langauges such as the handlebars or moustache
syntax.

## Directives: Conditional Rendering

We've renderd all todos, but lets make a list of todos. We'll do this using
directives.  The directive we'll be using is `v-for`. Let's refactor our code
a bit and it should become clear what our directive will be doing.

In the `<template>` tag put the following html:

```html
  <div id="todo">
    <ol>
      <li v-for="todo in todos"> {{todo.title}} {{todo.completed}}</li>
    </ol>
  </div>
```

When we refresh our app you'll see that the todos are now listed in order.

The `v-for` directive iterated through any iterable and each element will be
available within the `v-for` block with the name assigned to it (in this case
`todo`).

## Events and passing data

Let's add a simple remote button to each of our todos as such:

```HTML
<li v-for="todo in todos"> {{todo}} <button>Done</button></li>
```

Inside our button tag we're going to add an handler for a click event with
`@click="handleTodos(todo)"`.  This will fire a method that we have yet to
write and pass that method the information from the `todo` item that was clicked.

## Event 2: Methods object and emits

Now that we have a click event that calls a method and passes it data we must
write the method that the data will be passed to and handle sending it to the
parent component.

*At this point you may wonder why we're passing data to the parent this is*
*becuase since we defined our `todos` in the parent doing any changes to the*
*data must be done on that level.*

Now let's define our methods object and our `handleTodos` method:

```js
methods:{
    handleTodos(todo){

    }
  },
```

You can see that I'm passing in a param called `todo`, this could be named
anything, but to keep things semantic we're going to be calling this param `todo`.

This `handleTodos` method will be fired whenever someone clicks our `@handleTodos`
event handler.

Since we have your todo item let's pass it to our parent component so we can
do some logic on it.  Inside our `handletodo` method add `this.$emit('doneTodo', todo)`

This will pass the event to the parent, along with the `todo`.

## Handeling passed actions

In the child component we emitted the data to the parent. We have to now tell
the parent to expect the action. In the parent component `<App>` in the line
where the child `<HelloWorld>` is render lets change it to the following:

```HTML
<HelloWorld @doneTodo="doneTodo" :todos="todos" />
```

The `@doneTodo="doneTodo"` will call the `doneTodo` method we have yet to write
in this component and implicitly pass the `todo` item we emitted from the child
component.

Now let's add the methods object to the `App` component and the `doneTodo` method
to that.

```js
methods:{
  doneTodo(todo){

  }
},
```

This now lets us perform some logic on the entire todo object stored in this
component.

We can start simple by doing something like:

```js
doneTodo(todo){
  todo.completed = !todo.completed
}
```

This will simply toggle the completed attribute of our todo.

Vue's reactivity will handle tracking which todo to alter for us, so no need for
complex logic to pull out the correct `todo` from our `todos` array.

Now on our page we can see the toggeling of the `completed` todo.

## Adding more directives

Now that we can toggle our `todos` lets add some more logic to our child component
`<HelloWorld>` to make things look a bit better.

We're going to use the vue class binding directive to add a stikethrough to
our completed todos.

In our child component `<li>` add the following inside the opening tag:

```html
:class="{'strikethrough':todo.completed}"
```

This will apply a class `strikethrough` if the `completed` attribute for a `todo`
element evualatues to `true`. Let's inspect this in the DOM to verify.

Now in our `<style>` tag lets add `<style scoped>` to prevent our CSS from leaking
to other components, and set and attribue to the `strikethrough` class:

```css
.strikethrough{
  text-decoration: line-through;
}
```

## Computeds

Being able to perform complex logic on data is key, but we want to keep this
logic out of our template because it can quickly become unweidly.

Let's display a list of all the todos that we have completed. (Typcally we would
create another componet to render this but for ease we're doing to do it in our
`App` component).

Let's define a `computed` object and put some code in it to render our completed
todos:

```js
computed:{
    todosDone(){
      return this.todos.filter(x => x.completed)
    }
  },
```

*Note: all computeds must end with a return*

What does the method above do:
1. filters the `todos` object define on the component
2. returns the result of the filter as `todosDone` which can be accessed anywhere
in the current component.

Now that we have defined our done todos, lets render it by adding `{{todosDone}}`
inside our `App` template.

Now we're rendering our todos.

_On your own:_ Try to render the completed todos as a list instead of an object.

## Watchers

Watchers in vue give us the ability to perform some logic after a piece of data
we are observing or "watching" has changed. In our case we want to dispay to the
user everytime a they have completed a todo.

First we need to define a `watcher` object and tell it what to watch, in our `App`
component:

```js
watch:{
  todosDone(){

  }
},
```

This tells Vue to look for any changes in our todo `todosDone` object.

*You may note that `todosDone` is a computed, you can watch for computeds, props,*
*data and other more complex items which we will not cover*

In our todosDone watcher method we want to do this:

```js
this.todoChange = true
      setTimeout(()=>{
        this.todoChange = false
      }, 2000)
```

and in our data we want to add the line:

```js
todoChange: false,
```

What is happening here?
1. Everytime the `todosDone` data is changed we fire our watcher.
2. We created a boolean data attribute called `todoChange` and set it's default
state to false.
3. When our watcher method gets fired we set `todoChange` to true, then 2000 milliseconds
later we set it back to false.

As of now we cannot see anything happening in our app so let's make use of this
new data attribute and watcher we just created by add the following to our template:

```HTML
<h2 v-if="todoChange">Todo Has changed</h2>
```

You'll notice we used the `v-if` directive.  The `v-if` directive will only render
the element if the condition inside the quotes evualatues to `true`.

## Wrap Up

We have successfully learned the basic concepts of Vue.

-  Watchers
-  Events
-  Directives
-  Props
-  Components

For further information and resources check out [Vue.js](https://vuejs.org/)
