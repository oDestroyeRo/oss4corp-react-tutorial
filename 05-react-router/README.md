## React Router

โดยปกติแล้วการใช้งานเว็บไซต์ที่มีมากกว่า 1 page จะเปลี่ยน page โดยใช้ url ที่แตกต่างกันเช่น

```
https://www.sampledomain.com/
https://www.sampledomain.com/register.html
```

เราสามารถทำแบบเดียวกันได้ใน ReactJs โดยใช้ `react-router-dom` * ในคลาสนี้เราจะใช้ `react-router-dom` version 4.x

เราสามารถติดตั้ง `react-router-dom` ได้ด้วยคำสั่ง

```
npm install react-router-dom --save
```

โดย Component ที่ต้องการใช้ router จะต้องเป็น children ของ `BrowserRouter`

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import { BrowserRouter } from 'react-router-dom'

import registerServiceWorker from './registerServiceWorker';


ReactDOM.render(
  <BrowserRouter>
    <App/>
  </BrowserRouter>
, document.getElementById('root'));
registerServiceWorker();
```


```javascript
/* pages/PostList.js */
import React, {Component} from 'react';

class PostList extends Component{
  render() {
    return (
      <div>
        <h2>Posts</h2>
        <ul>
          <li>Post 1</li>
          <li>Post 2</li>
          <li>Post 3</li>
        </ul>
      </div>
    );
  }
}
export default PostList;
```

เพื่อแสดงผล Component อื่นๆใน `App` เราจะแก้ไขโค้ดดังนี้

```javascript
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

import {Link, Switch} from 'react-router-dom';

import Welcome from './Welcome'
import PostList from './pages/PostList'
import AlbumList from './pages/AlbumList'


class App extends Component {
  render() {
    const numbers = [1, 2, 3, 4, 5];
    const listItems = numbers.map((number) =>
      <li>{number}</li>
    );
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h1 className="App-title">Welcome to React</h1>
        </header>
        <div>
          <Link to="/">Home</Link>,
          <Link to="/posts">Posts</Link>,
          <Link to="/albums">Albums</Link>
        </div>
        <div style={{textAlign:'left', padding:'10px'}}>
			<Switch>
				<Route path="/" exact component={Welcome} />
				<Route path="/posts" component={PostList} />
				<Route exact path="/albums" component={AlbumList} />
			</Switch>
        </div>
      </div>
    );
  }
}

export default App;
```

หากต้องการส่ง Paramter ไปยัง Component สามารถส่งผ่าน url ได้โดย

```javascript
<Route path="/posts/:id" component={PostList} />
```

ใน Compnent จะสามารถรับ parameter ได้จาก props

```javascript
/* pages/PostList.js */
this.props.match.params.id

```

