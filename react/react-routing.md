# How to install and using react routing

1. Install following packages

```
npm install react-router-dom --save
```

2. Usually you should create a separate component used for application routing

```js
import React, { Component } from 'react';
import { Route, Switch } from 'react-router-dom';

import Home from './components/Home/home';
import Layout from './hoc/Layout/layout';
import News from './path/to/News';
import About from './path/to/About';


class Routes extends Component {
    render() {
        return (
            <Layout>
                <Switch>                    
                    <Route path="/" exact component={Home}/>
                    <Route path="/news/:id" exact component={News} />
                    <Route path="/videos/:id" exact component={About} />
                </Switch>
            </Layout>
        );
    }
}

export default Routes;
```

Here `Layout` is just a hoc

3. In your entry component, use `BrowserRouter`

```js
import React, { Component } from 'react';
import { BrowserRouter } from 'react-router-dom';
import Routes from './routes';

class App extends Component {
  render() {
    return (
      <BrowserRouter>
        <Routes/>
      </BrowserRouter>
    );
  }
}

export default App;
```

4. In any components you'd like to get routing works, use `Link` component

```js
import { Link } from 'react-router-dom';

<Link to="/" className="logo">Logo</Link>
```

`<Link>`s use the to prop to describe the location that they should navigate to. This can either be a string or a location object (containing a combination of `pathname`, `search`, `hash`, and `state` properties). When it is a string, it will be converted to a location object.

```
<Link to={{ pathname: '/post/1' }}>Post #1</Link>

// a basic location object
{ pathname: '/', search: '', hash: '', key: 'abc123' state: {} }
```

### You can get routing value via props

```
```
