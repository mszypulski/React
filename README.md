
# React in a pill
written by Mariusz Szypulski

## Starting files

### index.html

This is just regular HTML, **div id = "app"** is a root element for our app and **index.js** script is bundled app file by webpack.

```javascript
<!DOCTYPE html>
<html lang = "en">

   <head>
      <meta charset = "UTF-8">
      <title>React App</title>
   </head>

   <body>
       <div id = "app"></div>
       <script src = "index.js"></script>
   </body>

</html>
```

### App.jsx

This is the first React component.

```javascript
import React from 'react';

class App extends React.Component {
   render() {
      return (
         <div>
            React is simple !!!
         </div>
      );
   }
}
export default App;
```

### main.js

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App.jsx';

ReactDOM.render(<App />, document.getElementById('app'));
```

This file rendering App component in '<div id="app">' of index.html, so we can see a string **React is simple !!!** in a browser.

## Using JSX

### app.jsx

We can wrap more elements with one **div** container element. 

```javascript
import React from 'react';

class App extends React.Component {
   render() {
      return (
         <div>
           <h1>Header</h1>
           <h2>Title</h2>
           <p>Text !!!</p>
         </div>
      );
   }
}
export default App;
```

### Custom attributes

We can add custom attribute using **data**-prefix.
```javascript
import React from 'react';

class App extends React.Component {
   render() {
      return (
         <div>
            <h1>Header</h1>
            <h2>Title</h2>
            <p data-myattribute = "value">This is a text !!!</p>
         </div>
      );
   }
}
export default App;
```
### Expressions

We can wrap expressions with curly brackets **{}**.
```javascript
import React from 'react';

class App extends React.Component {
   render() {
      return (
         <div>
            <h1>{2*2}</h1>
         </div>
      );
   }
}
export default App;
```
We can use conditional expression as well.
```javascript
import React from 'react';

class App extends React.Component {
   render() {
      var i = 0;
      return (
         <div>
            <h1>{i == 0 ? 'True!' : 'False'}</h1>
         </div>
      );
   }
}
export default App;
```
### Inline Styles

When we want to set inline styles, we need to use **camelCase** syntax.
```javascript
import React from 'react';

class App extends React.Component {
   render() {
      var inlineStyle = {
         fontSize: 100,
         color: '#FF0000'
      }
      return (
         <div>
            <h1 style = {inlineStyle}>Header</h1>
         </div>
      );
   }
}
export default App;
```
### Comments

We can writing comments with '//' for one line comment and '/* .. */' for multi line comment.
```javascript
import React from 'react';

class App extends React.Component {
   render() {
      return (
         <div>
            <h1>Header</h1>
            {
             //End of the line Comment...
            }
            { 
               /*
               Multi 
               line 
               comment
               ...*/
            }
         </div>
      );
   }
}
export default App;
```
### Components

The **App** component is owner of **Header** and **Content** component.
```javascript
import React from 'react';

class App extends React.Component {
   render() {
      return (
         <div>
            <Header/>
            <Content/>
         </div>
      );
   }
}
class Header extends React.Component {
   render() {
      return (
         <div>
            <h1>Header</h1>
         </div>
      );
   }
}
class Content extends React.Component {
   render() {
      return (
         <div>
            <h2>Content</h2>
            <p>The content text!!!</p>
         </div>
      );
   }
}
export default App;
```
## State

State is the place where the data comes from.
### Stateful Component

In this example, we will set the state for owner component (App). We are creating table and tbody elements, where we will dynamically insert TableRow for every object from the data array.

```javascript
import React from 'react';

class App extends React.Component {
   constructor() {
      super();
      this.state = {
         data: 
         [
            {
               "id":1,
               "name":"Andrew",
               "age":"20"
            },
            {
               "id":2,
               "name":"Barbara",
               "age":"30"
            },
            {
               "id":3,
               "name":"John",
               "age":"40"
            }
         ]
      }
   }
   render() {
      return (
         <div>
            <Header/>
            <table>
               <tbody>
                  {this.state.data.map((person, i) => 
                  <TableRow key = {i} data = {person} />)}
               </tbody>
            </table>
         </div>
      );
   }
}
class Header extends React.Component {
   render() {
      return (
         <div>
            <h1>Header</h1>
         </div>
      );
   }
}
class TableRow extends React.Component {
   render() {
      return (
         <tr>
            <td>{this.props.data.id}</td>
            <td>{this.props.data.name}</td>
            <td>{this.props.data.age}</td>
         </tr>
      );
   }
}
export default App;
```
### Props
```javascript
import React from 'react';

class App extends React.Component {
   constructor(props) {
      super(props);
		
      this.state = {
         header: "Header from state...",
         content: "Content from state..."
      }
   }
   render() {
      return (
         <div>
           <h1>{this.state.header}</h1>
           <h2>{this.state.content}</h2>
         </div>
      );
   }
}
export default App;
```
 The child components should only pass data from the state using props.
```javascript
import React from 'react';

class App extends React.Component {
   constructor(props) {
      super(props);
      this.state = {
         header: "Header from props...",
         content: "Content from props..."
      }
   }
   render() {
      return (
         <div>
            <Header headerProp = {this.state.header}/>
            <Content contentProp = {this.state.content}/>
         </div>
      );
   }
}
class Header extends React.Component {
   render() {
      return (
         <div>
            <h1>{this.props.headerProp}</h1>
         </div>
      );
   }
}
class Content extends React.Component {
   render() {
      return (
         <div>
            <h2>{this.props.contentProp}</h2>
         </div>
      );
   }
}
export default App;
```
### Default Props
```javascript
import React from 'react';

class App extends React.Component {
   render() {
      return (
         <div>
            <h1>{this.props.headerProp}</h1>
            <h2>{this.props.contentProp}</h2>
         </div>
      );
   }
}
App.defaultProps = {
   headerProp: "Header from props...",
   contentProp:"Content from props..."
}
export default App;
```
### API
## setState()

Method **setState()** is used to add changes to the original state of the component.
```javascript
import React from 'react';

class App extends React.Component {
   constructor() {
      super();
		
      this.state = {
         data: []
      }
	
      this.setStateHandler = this.setStateHandler.bind(this);
   };
   setStateHandler() {
      var item = "setState "var myArray = this.state.data.slice();
	  myArray.push(item);
      this.setState({data: myArray})
   };
   render() {
      return (
         <div>
           <button onClick = {this.setStateHandler}>SET STATE</button>
           <h4>State Array: {this.state.data}</h4>
         </div>
      );
   }
}
export default App;
```
## forceUpdate()

Method **forceUpdate()** is used to update the component.
```javascript
import React from 'react';

class App extends React.Component {
   constructor() {
      super();
      this.forceUpdateHandler = this.forceUpdateHandler.bind(this);
   };
   forceUpdateHandler() {
      this.forceUpdate();
   };
   render() {
      return (
         <div>
          <button onClick = {this.forceUpdateHandler}>FORCE UPDATE</button>
          <h4>Random number: {Math.random()}</h4>
         </div>
      );
   }
}
export default App;
```
## ReactDOM.findDOMNode()

Method **ReactDOM.findDOMNode()** is used to find a DOM node.
```javascript
import React from 'react';
import ReactDOM from 'react-dom';

class App extends React.Component {
   constructor() {
      super();
      this.findDomNodeHandler = this.findDomNodeHandler.bind(this);
   };
   findDomNodeHandler() {
      var myDiv = document.getElementById('myDiv');
      ReactDOM.findDOMNode(myDiv).style.color = 'green';
   }
   render() {
      return (
         <div>
         <button onClick = {this.findDomNodeHandler}>FIND DOME NODE</button>
         <div id = "myDiv">NODE</div>
         </div>
      );
   }
}
export default App;
```
## Component Life Cycle Methods

- **componentWillMount** is executed before rendering, on both the server and the client side.
- **componentDidMount** is executed after the first render only on the client side.
- **componentWillReceiveProps** is invoked as soon as the props are updated before another render is called.
- **shouldComponentUpdate** should return true or false value. This will determine if the component will be updated or not. This is set to true by default. If you are sure that the component doesn't need to render after state or props are updated, you can return false value.
- **componentWillUpdate** is called just before rendering.
- **componentDidUpdate** is called just after rendering.
- **componentWillUnmount** is called after the component is unmounted from the dom.

### Input Form

Updating the state whenever the input value changes.
```javascript
import React from 'react';

class App extends React.Component {
   constructor(props) {
      super(props);
      
      this.state = {
         data: 'Initial data...'
      }
      this.updateState = this.updateState.bind(this);
   };
   updateState(e) {
      this.setState({data: e.target.value});
   }
   render() {
      return (
         <div>
            <input type = "text" value = {this.state.data} 
               onChange = {this.updateState} />
            <h4>{this.state.data}</h4>
         </div>
      );
   }
}
export default App;
```
### Input Form in Child Component

Whenever we need to update state from child component, we need to pass the function that will handle updating as a prop.
```javascript
import React from 'react';

class App extends React.Component {
   constructor(props) {
      super(props);
      
      this.state = {
         data: 'Initial data...'
      }
      this.updateState = this.updateState.bind(this);
   };
   updateState(e) {
      this.setState({data: e.target.value});
   }
   render() {
      return (
         <div>
            <Content myDataProp = {this.state.data} 
               updateStateProp = {this.updateState}>
            </Content>
         </div>
      );
   }
}
class Content extends React.Component {
   render() {
      return (
         <div>
            <input type = "text" value = {this.props.myDataProp} 
               onChange = {this.props.updateStateProp} />
            <h3>{this.props.myDataProp}</h3>
         </div>
      );
   }
}
export default App;
```
## Events

**onClick** event will trigger **updateState** function when the button is clicked.
```javascript
import React from 'react';

class App extends React.Component {
   constructor(props) {
      super(props);
      
      this.state = {
         data: 'Initial data...'
      }
      this.updateState = this.updateState.bind(this);
   };
   updateState() {
      this.setState({data: 'Data updated...'})
   }
   render() {
      return (
         <div>
         <button onClick = {this.updateState}>CLICK</button>
         <h4>{this.state.data}</h4>
         </div>
      );
   }
}
export default App;
```
### Child Events
```javascript
import React from 'react';

class App extends React.Component {
   constructor(props) {
      super(props);
      
      this.state = {
         data: 'Initial data...'
      }
      this.updateState = this.updateState.bind(this);
   };
   updateState() {
    this.setState({data: 'Data updated from the child component...'})
   }
   render() {
      return (
         <div>
            <Content myDataProp = {this.state.data} 
               updateStateProp = {this.updateState}></Content>
         </div>
      );
   }
}
class Content extends React.Component {
   render() {
      return (
         <div>
         <button onClick = {this.props.updateStateProp}>CLICK</button>
         <h3>{this.props.myDataProp}</h3>
         </div>
      );
   }
}
export default App;
```
## Refs

**ref** is used to return a reference to the element.
```javascript
import React from 'react';
import ReactDOM from 'react-dom';

class App extends React.Component {
   constructor(props) {
      super(props);
		
      this.state = {
         data: ''
      }
      this.updateState = this.updateState.bind(this);
      this.clearInput = this.clearInput.bind(this);
   };
   updateState(e) {
      this.setState({data: e.target.value});
   }
   clearInput() {
      this.setState({data: ''});
      ReactDOM.findDOMNode(this.refs.myInput).focus();
   }
   render() {
      return (
         <div>
           <input value = {this.state.data} 
           onChange = {this.updateState} 
           ref = "myInput"></input>
           <button onClick = {this.clearInput}>CLEAR</button>
           <h4>{this.state.data}</h4>
         </div>
      );
   }
}
export default App;
```
## Keys

Setting the **key** value will keep your components uniquely identified after the change. React will use the **key** values to keep track of each element.
```javascript
import React from 'react';

class App extends React.Component {
   constructor() {
      super();
		
      this.state = {
         data:[
            {
               component: 'First...',
               id: 1
            },
            {
               component: 'Second...',
               id: 2
            },
            {
               component: 'Third...',
               id: 3
            }
         ]
      }
   }
   render() {
      return (
         <div>
            <div>
               {this.state.data.map((dynamicComponent, i) => <Content 
                  key = {i} componentData = {dynamicComponent}/>)}
            </div>
         </div>
      );
   }
}
class Content extends React.Component {
   render() {
      return (
         <div>
            <div>{this.props.componentData.component}</div>
            <div>{this.props.componentData.id}</div>
         </div>
      );
   }
}
export default App;
```
