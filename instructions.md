# Exercise 1: Hello world
There are a few building blocks to get started with React.

1. React needs a container to render into
    - `document.getElementById('container')`
1. You need to declare what you would like to render. You do this with the `React.createElement` method. It takes 3 arguments, but we will leave the second one until later. The first is the element name, the third is the children of that element. Use the code below to render Hello world in an `<h1>` tag.  
    ``` js
    React.createElement('h1', null, 'Hello world')
    ```
1. Finally you need to render your element into the container using the `ReactDOM.render(element, container)` method.

# Exercise 2: Multiple children
In exercise 1 we simply set the children property to a string and it rendered. You can also nest elements.

1. Change the structure of the output to be  
    ``` html
    <div>
        <h1>Hello world</h2>
    </div>
    ```
1. Then introduce another child to get the rendered output to be  
    ``` html
    <div>
        <h1>Hello world</h2>
        <p>React is pretty awesome</p>
    </div>
    ```

# Exercise 3: Properties (new)
Next we want to introduce an anchor for our heading so it can be linked to.

    ``` html
    <div>
        <h1><a id="hello-world" />Hello world</h2>
        <p>React is pretty awesome</p>
    </div>
    ```

The second argument of `React.createElement` can accept attributes which will be added to the rendered html element.

**Important:** The naming convention for properties is always *camelCased*. For example `maxLength` and `tabIndex`

Solution:
``` js
var HelloWorld = React.createElement('div', {
    children: [
        React.createElement('h1', { children: [
            React.createElement('a', { id: 'hello-world' }),
            'Hello world' 
        ]}),
        React.createElement('p', { children: 'React is pretty awesome' })
    ]
});
```

# Exercise 4: Events (new)
React has an synthetic event system. This means you can subscribe to events on any element.

Your task is to handle a click event on the text 'React is pretty awesome'.

Like properties events are named using *camelCasing*, eg `onClick`.

Solution:
``` js
var HelloWorld = React.createElement('div', {
    children: [
        React.createElement('h1', { children: [
            React.createElement('a', { id: 'hello-world' }),
            'Hello world' 
        ]}),
        React.createElement('p', {
            children: 'React is pretty awesome',
            onClick: function() { console.log('Hi!') }
        })
    ]
});
```

# Exercise 5: React Classes
We can now render html, the next step is to encapsulate our elements into a reusable component. 

We do this with the `React.createClass(specification)` method.

The `specification` argument has one mandatory property: `render`. It must return a *single* react element.

``` js
var HelloWorld = React.createClass({
    render: function() {
        return React.createElement('h1', null, 'Hello world')
    }
})
```

Once you have created your React Class you can use the `React.createElement` method to render it. `React.createElement(HelloWorld)`.

Convert your existing code to encapsulate the HelloWorld element into a class then render it.

# Exercise 6: State
No application can exist without state. We are going to push our hello world a bit further before switching to a more in depth exercise.

We are going to add a simple counter which will increment when we click on the 'React is pretty awesome' paragraph.

First our element needs some initial state. Your class can declare it's initial state by adding a `getInitialState` function to the class specification.

``` js
{
    render: function() { return ... }
    getInitialState: function() { return { clicks: 0 } }
}
```

You can access state in your component through `this.state`, for example: `this.state.clicks`.

To update state you call `setState(updates)` with the state changes. For example to increment the counter we would do `setState({ clicks: this.state.clicks + 1 })`

Now update your hello world to output `React is pretty awesome: {number clicks}`. 
