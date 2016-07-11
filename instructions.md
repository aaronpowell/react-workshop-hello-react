# Exercise 1: Hello world
There are a few building blocks to get started with React.

1. The first step to hello world in react is declaring what you want to render. You do this with the `React.createElement` method. It takes 3 arguments, but we will leave the second one until later. The first is the element name, the third is the children of that element. Use the code below to render Hello world in an `<h1>` tag.  
    ``` js
    React.createElement('h1', null, 'Hello world')
    ```
1. React needs a container to render into  
    ``` js
    document.getElementById('container')
    ```
1. Finally you need to render your element into the container using the `ReactDOM.render(element, container)` method.

# Exercise 2: Multiple children
In exercise 1 we passed a string to the third argument *children*. You can also pass other *React Elements* returned from `React.createElement`

1. Change the structure of the output to be  
    ``` html
    <div>
        <h1>Hello world</h2>
    </div>
    ```
1. Then introduce another child to get the rendered output to be (tip, try passing a p Element as a 4th argument)  
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

**Important:** The naming convention for properties (including all html properties) is always *camelCased*. For example `maxLength` and `tabIndex`

# Exercise 4: Events (new)
React has an synthetic event system. This means you can subscribe to events on any element.

Your task is to handle a click event on the text 'React is pretty awesome' and print something to the `console`.

Events, the same as properties, are named using *camelCasing*, eg `onClick`.

**Note** Make sure you have the browser dev tools open to test your solution.

# Exercise 5: React Classes
We can now render html, the next step is to encapsulate our elements into a reusable component. 

We do this with the `React.createClass(specification)` method.

The `specification` argument has one mandatory property: `render`. It must return a *single* react element.

``` js
var HelloWorld = React.createClass({
    render: function() {
        return React.createElement(...)
    }
})
```

Once you have created your React Class you can use the `React.createElement` method to render it. `React.createElement(HelloWorld)`.

Convert your existing code to encapsulate the HelloWorld element into a class then render it.

If you have the React DevTools installed in [Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) or [Firefox](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/) you will notice that your class is called `<Constructor>`. This is not very helpful, lets add a `displayName: HelloWorld` property to our class and see the difference.

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
In step 4, you would have declared an anonymous function, the scope of `this` will be wrong for the callback, if you move your handler onto your createClass specification it will bind to the instance *automatically*.

Now update your hello world to output `React is pretty awesome: {number clicks}`. 

# Exercise 7: JSX
You may have heard people talking about JSX and seen some examples of it around. JSX removes the need for createElement calls.

To convert to JSX we need to include another dependency. Add this script under the react scripts and chance the script type to `text/babel`

``` html
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.min.js"></script>
    <script type='text/babel'>
        // Your code
    </script>
```

To convert to JSX:
1. Replace the `React.createElement(` with an `<`.
    - `React.createElement('div', { id: 'myId' }, 'Hi')`
    - becomes
    - `<'div' { id: 'myId' }, 'Hi')`
2. Remove the quotes if it is a built in html type
    - `<'div' { id: 'myId' }, 'Hi')`
    - becomes
    - `<div { id: 'myId' }, 'Hi')`
3. The second argument then gets turned into xml attributes
    - `<div { id: 'myId' }, 'Hi')`
    - becomes
    - `<div id='myId', 'Hi')`
    - **Notes**
        - Strings are quoted
        - JavaScript (like the this.clicked callback) need to be surrounded with braces, like `onClick={this.clicked}`
4. Next replace the comma with a closing greater than sign.
    - `<div id='myId', 'Hi')`
    - becomes 
    - `<div id='myId'>'Hi')`

5. Then nest the children directly under your element
    - `<div id='myId'>'Hi')`
    - becomes 
    ```
    <div id='myId'>
        Hi
    )
    ```
    - **Notes**
        - Any `React.createElement` calls will also have to be converted to JSX
        - If you are using JavaScript, like `'React is awesome' + this.state.clicks`, you need to surround it with braces to enter 'JavaScript mode'. i.e `<p>{'React is awesome ' + this.state.clicks}</p>`
        - Strings do not need to be quoted
6. Turn the final close paren `)` into a closing xml tag
    ```
    <div id='myId'>
        Hi
    )
    ```
    - becomes 
    ```
    <div id='myId'>
        Hi
    </div>
    ```

Try converting your Hello World app into JSX. Then decide which you like better?

Remember JSX is *completely optional*, it is just a pre-processor which can make your html markup look more familiar and easier to parse visually.