# How to install and using react routing

1. Install following packages

```
npm install react-dom react-router-dom --save
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

### You can get routing value via props