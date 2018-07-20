## Rendering Elements

จาก `create-react-app` เราจะพบไฟล์ App.js โดยมีรายละเอียดดังนี้

```javascript
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h1 className="App-title">Welcome to React</h1>
        </header>
        <p className="App-intro">
          To get started, edit <code>src/App.js</code> and save to reload.
        </p>
      </div>
    );
  }
}

export default App;
```

เราสามารถเพิ่ม/แก้ไขการแสดงผลได้ เช่นเพิ่มข้อความผ่านตัวแปรดังนี้

```javascript
class App extends Component {
  render() {
	 const element = <h1>Hello, world</h1>;
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h1 className="App-title">Welcome to React</h1>
        </header>
        <p className="App-intro">
        {element}
        </p>
      </div>
    );
  }
}
```

## Components and Props
การพัฒนา App ด้วย ReactJS นั้นจะทำโดยสร้าง Component ขึ้นมาใหม่ แล้วนำ Component นั้นๆมาประกอบรวมกัน

### Functional and Class Components
โค้ดตัวอย่างของ Component

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
หรือจะเขียนในรูปแบบ ES6 Class ก็ได้ซึ่งโค้ดจะมีรูปแบบดังนี้

```javascript
class Welcome extends Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

ลองทดสอบ component นี้กับ App.js ในโปรเจคดังนี้

```javascript
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class Welcome extends Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h1 className="App-title">Welcome to React</h1>
        </header>
        <p className="App-intro">
          <Welcome name="OSS4CORP"/>
        </p>
      </div>
    );
  }
}

export default App;
```

จะสังเกตุว่าเราเพิ่ม class Welcome เข้าไปก่อนหน้า class App และเรียกใช้ Welcome ในรูปแบบ JSX ในหน้าเว็บจะแสดงผลว่า "Hello, OSS4CORP" (หรือค่าอื่นๆที่เราใส่ผ่านตัวแปร name)

โดยตัวแปร `name` นั้นจะคือตัวแปรแบบ `props`

เพื่อลดความซ้ำซ้อนของโค้ดตัวอย่าง เราจะย้าย Welcome ไปที่ Welcome.js ซึ่งมีรายละเอียดดังนี้

```javascript
/* Welcome.js */
import React, { Component } from 'react';
class Welcome extends Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
export default Welcome;
```

และใน App.js จะเรียกใช้ Welcome ด้วยการ import

```javascript
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';
import Welcome from './Welcome';
```

## State and Lifecycle
`state` เป็นตัวแปรที่สำคัญอีกประเภท เนื่องจาก Component ใน React จะมีการตรวจสอบการเปลี่ยนแปลงของตัวแปรประเภทนี้ว่ามีผลต่อการแสดงผลหรือใหม่ หาก state มีการเปลี่ยนแปลงที่มีผลกระทบจากหน้าจอ Component จะทำการ render Component ใหม่ (เฉพาะจุดที่อับเดท)

ตัวอย่างเช่น

```javascript
/* Welcome.js */
import React, { Component } from 'react';
class Welcome extends Component {
  constructor(props){
    super(props);
    this.state = {now: new Date().toLocaleString()};
  }
  render() {
    const {now} = this.state;
    return (
      <div>
        <h1>Hello, {this.props.name}</h1>
        <p>Now is : {now}</p>
      </div>
    )
  }
}
export default Welcome;
```
ตัวอย่างนี้ได้ทำการเพิ่มเวลาที่แสดงผลในหน้าจอเข้าไปในตัวแปร state เมื่อมีการเปิด web page ใหม่หน้าจอจะทำการแสดงเวลาที่กำการเปิดเพจนั้นๆ และเนื่องจากไม่มีการแก้ไขค่าใดๆ Component จะทำการ `render()` เพียงครั้งเดียว

ตัวอย่างถัดไปแสดงให้เห็นถึงวิธีการอับเดท `state` และผลลัพทธ์ที่เกิดขึ้นในหน้าจอ

```javascript
/* Welcome.js */
import React, { Component } from 'react';
class Welcome extends Component {
  constructor(props){
    super(props);
    this.state = {now: new Date()};
    setInterval(this.tick, 1000);
  }
  tick = () => {
    this.setState({
      now: new Date(),
    });
  }
  render() {
    const {now} = this.state;
    return (
      <div>
        <h1>Hello, {this.props.name}</h1>
        <p>Now is : {now.toLocaleString()}</p>
      </div>
    )
  }
}

export default Welcome;

```

จากตัวอย่างจะมีการเรียก method `tick` ทุกๆ 1 วินาทีเพื่อเปลี่ยนแปลงค่า `now` ซึ่งเป็นตัวแปรประเภท `state` component จึงจำเป็นต้อง `render()` ใหม่ทุกๆ 1 วินาที

**Note** ถึงแม้ว่าจะมีการเรียก `render()` ใหม่ทุก 1 วินาที แต่ ReactJS ไม่ได้อับเดทหน้าจอของ Component ทั้งหมด โดย class Component จะมีตัวตรวจสอบและควบคุมให้เปลี่ยนแปลงเฉพาะจุดเท่านั้น

การเรียกใช้งานตัวแปร `state` ใน render นั้นสามารถทำได้โดยตรงเช่น

```javascript
<p>Now is : {this.state.now.toLocaleString()}</p>
```


## Handling Events
โดยปกติ javascript สามารถจัดการ Event ได้ดังตัวอย่าง

```javascript
<a href="#" onclick="console.log('The link was clicked.'); return false">
  Click me
</a>
```

แต่ใน ReactJS นั้นเราจะใช้รูปแบบของ JSX ซึ่งอาจเขียนได้ดังนี้

```javascript
function handleClick(e) {
	e.preventDefault();
   console.log('The link was clicked.');
}

<a href="#" onClick={handleClick}>
	Click me
</a>
```
ตัวอย่างของการจัดการ Event ใน Component

```javascript
/* Counter.js */
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props){
    super(props);
    this.state = {counter: 0};
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    const counter = this.state.counter + 1;
    this.setState({counter});
  }

  render() {
    const {counter} = this.state;
    return (
      <div>
        Click: {counter}<br/>
        <button type="button" onClick={this.handleClick}>Button</button>
      </div>
    )
  }
}
export default Counter;
```

จะสังเกตุได้ว่าเราต้องทำการ `bind` event ทุกครั้งใน constructor หากจำนวน Event มีมากอาจทำให้โค้ดดูยากขึ้น ซึ่งเราสามารถข้ามการ `bind` ด้วยการปรับโค้ดให้เป็นดังนี้

```javascript
/* Counter.js */
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props){
    super(props);
    this.state = {counter: 0};
  }
  handleClick = () => {
    const counter = this.state.counter + 1;
    this.setState({counter});
  }

  render() {
    const {counter} = this.state;
    return (
      <div>
        Click: {counter}<br/>
        <button type="button" onClick={this.handleClick}>Button</button>
      </div>
    )
  }
}

export default Counter;
```
ตัวอย่างอื่นๆ จาก [reactjs.org](https://reactjs.org/)

```javascript
class TodoApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = { items: [], text: '' };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  render() {
    return (
      <div>
        <h3>TODO</h3>
        <TodoList items={this.state.items} />
        <form onSubmit={this.handleSubmit}>
          <label htmlFor="new-todo">
            What needs to be done?
          </label>
          <input
            id="new-todo"
            onChange={this.handleChange}
            value={this.state.text}
          />
          <button>
            Add #{this.state.items.length + 1}
          </button>
        </form>
      </div>
    );
  }

  handleChange(e) {
    this.setState({ text: e.target.value });
  }

  handleSubmit(e) {
    e.preventDefault();
    if (!this.state.text.length) {
      return;
    }
    const newItem = {
      text: this.state.text,
      id: Date.now()
    };
    this.setState(prevState => ({
      items: prevState.items.concat(newItem),
      text: ''
    }));
  }
}

class TodoList extends React.Component {
  render() {
    return (
      <ul>
        {this.props.items.map(item => (
          <li key={item.id}>{item.text}</li>
        ))}
      </ul>
    );
  }
}
```

```javascript
class MarkdownEditor extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = { value: 'Hello, **world**!' };
  }

  handleChange(e) {
    this.setState({ value: e.target.value });
  }

  getRawMarkup() {
    const md = new Remarkable();
    return { __html: md.render(this.state.value) };
  }

  render() {
    return (
      <div className="MarkdownEditor">
        <h3>Input</h3>
        <label htmlFor="markdown-content">
          Enter some markdown
        </label>
        <textarea
          id="markdown-content"
          onChange={this.handleChange}
          defaultValue={this.state.value}
        />
        <h3>Output</h3>
        <div
          className="content"
          dangerouslySetInnerHTML={this.getRawMarkup()}
        />
      </div>
    );
  }
}
```

**Tip** Event ใน ReactJS นั้นจะใช้เหมือนกันกับ Event ของ HTML สามารถดูรายละเอียดเพิ่มเติมได้ที่ [https://www.w3schools.com/tags/ref_eventattributes.asp](https://www.w3schools.com/tags/ref_eventattributes.asp)


## Conditional Rendering
ใน Component นั้นเราสามารถสร้างเงื่อนไขในการ `return` ได้ เช่นเมื่อเราต้องการเลือกที่จะข้อความแจ้งให้ Login หรือแจ้งข้อความยินดีต้อนรับสำหรับสมาชิกที่ Login แล้ว

```javascript
function UserGreeting(props) {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
  return <h1>Please sign up.</h1>;
}
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}
ReactDOM.render(
  // Try changing to isLoggedIn={true}:
  <Greeting isLoggedIn={false} />,
  document.getElementById('root')
);
```

**Tip** หากเราต้องการสร้าง Component ที่ไม่จำเป็นต้องมี Logic เราสามารถใช้ function แทนได้ดังตัวอย่างข้างต้น ทั้งนี้หากเราต้องการเขียนโค้ดให้อยู่ในรูปแบบมาตรฐานของ ReactJS (ใช้ `()` แทน function) เราสามารถปรับโค้ดได้ดังนี้

```javascript
const UserGreeting = (props) => {
  return <h1>Welcome back!</h1>;
}
```
หรือตัด `return` ออกเพื่อให้โค้ดกระชับขึ้น

```javascript
const UserGreeting = (props) => (
  <h1>Welcome back!</h1>
)
```


### Inline If with Logical && Operator
เราสามารถใช้ expression ใน JSX เพื่อกำหนดเงื่อนไขในการแสดงผลได้

```javascript
const Greeting = (props) => (
	props.isLoggedIn ? <UserGreeting /> : <GuestGreeting />
)
```
หรือใช้ syntax แบบใหม่ที่ออกแบบมากับ JSX `true && expression`

```javascript
const Greeting = (props) => (
<div>
	{props.isLoggedIn && <UserGreeting />}
    {!props.isLoggedIn && <GuestGreeting />}
</div>
)
```

## Lists and Keys

ก่อนหน้านี้ได้มีการพูดถึงการใช้ `map` แทน forloop เช่น

```javascript
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number * 2);
console.log(doubled);
//[2, 4, 6, 8, 10]
```

เมื่อนำมาประยุกต์ใช้กับ JSX จะมีตัวอย่างดังนี้

```javascript
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);
//render() { 
//	return <ul>{listItems}</ul>
//}
```

เนื่องจาก ReactJS ได้แนะนำให้ tags ที่แสดงผลเป็น list ควรมี attribute key กำกำัเสมอ

```javascript
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>{number}</li>
);
```

## Forms

รูปแบบ form ทั่วไปของ HTML จะถูกจัดการโดย Web Browser (validate, submit)

```javascript
<form>
  <label>
    Name:
    <input type="text" name="name" />
  </label>
  <input type="submit" value="Submit" />
</form>
```

แต่ใน ReactJS นั้นเราควรใช้ state และจัดการด้วย Component ดังเช่น

```javascript
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```
โดย state จะมีการเปลี่ยนค่าเมื่อมีการพิมพ์ข้อความด้วย `handleChange`

### The textarea Tag
textarea นั้นปกติจะกำหนดค่าลงไปใน children

```javascript
<textarea>
  Hello there, this is some text in a text area
</textarea>
```

แต่ใน ReactJS นั้นได้ทำการแก้ไข tags textarea ให้รับค่าผ่านทาง attribute `value` แทน ดังตัวอย่าง

```javascript
class EssayForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 'Please write an essay about your favorite DOM element.'
    };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('An essay was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Essay:
          <textarea value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```



## Lifting State Up

## Composition vs Inheritance

## Thinking In React


### Reference
[https://reactjs.org/docs/ link](https://reactjs.org/docs/hello-world.html)