# Try React
***

ตัวอย่างของ [React Single File](https://raw.githubusercontent.com/reactjs/reactjs.org/master/static/html/single-file-example.html)

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello World</title>
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    
    <!-- Don't use this in production: -->
    <script src="https://unpkg.com/babel-standalone@6.15.0/babel.min.js"></script>
  </head>
  <body>
    <div id="root"></div>
    <script type="text/babel">

      ReactDOM.render(
        <h1>Hello, world!</h1>,
        document.getElementById('root')
      );

    </script>
    <!--
      Note: this page is a great way to try React but it's not suitable for production.
      It slowly compiles JSX with Babel in the browser and uses a large development build of React.

      Read this section for a production-ready setup with JSX:
      http://reactjs.org/docs/add-react-to-a-website.html#add-jsx-to-a-project

      In a larger project, you can use an integrated toolchain that includes JSX instead:
      http://reactjs.org/docs/create-a-new-react-app.html

      You can also use React without JSX, in which case you can remove Babel:
      https://reactjs.org/docs/react-without-jsx.html
    -->
  </body>
</html>
```

โดย web browser จะแสดงตัวอักษร Hello world และโค้ดที่จัดการการแสดงผลนั้นจะมีรูปแบบดังนี้

```javascript
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```

โดย paramter ที่ส่งไปยัง ReactDOM.render นั้นจะประกอบด้วย

* ค่าที่ต้องการแสดงผลในรูปแบบ string หรือ JSX
* object ที่ต้องการเขียนค่าลงไป

JSX ตัวแปรรูปแบบใหม่ที่สร้างขึ้นมาใช้ในการพัฒนาเว็บด้วย React, โดย JSX จะถูกแปลงเป็น HTML ในหน้าผลลัพธ์ เราสามารถสร้างตัวแปร JSX ได้ดังนี้

```javascript
const helloJSX = <h1>Hello, world!</h1>;
ReactDOM.render(
  helloJSX,
  document.getElementById('root')
);
```
หรือเขียน function ที่คืนค่าเป็น JSX

```javascript
function message() {
	return <h1>Hello, world!</h1>;
}
ReactDOM.render(
	message(),
	document.getElementById('root')
);
```

โดยตัวแปรแบบ JSX นั้นต้องมีค่าอยู่ใน Tags เดียวเท่านั้นเช่น

```javascript
const helloJSX = <h1>Hello, World!</h1><p>My name is ...</p>;
//Incorrect
```
`helloJSX` จะไม่สามารถใช้งานได้เนื่องจากเป็นตัวแปรที่ไม่ถูกต้อง หากต้องการแสดงผลหลาย Tags เราสามารถทำได้โดยเพิ่ม Tags ที่สามารถคลุม Tags ย่อยที่เราต้องการใช้ได้เช่น `<div>`

```javascript
const helloJSX = <div><h1>Hello, World!</h1><p>My name is ...</p></div>;
//Correct
```

และเรายังสามารถเว้นบรรทัดให้โค้ดอ่านได้ง่ายขึ้น ผลลัพธ์ไม่เปลี่ยนแปลงได้ดังนี้

```javascript
const helloJSX = (
	<div>
		<h1>Hello, World!</h1>
		<p>My name is ...</p>
	</div>
);
```


## Embedding Expressions in JSX
JSX นั้นยังสามารถใส่คำสั่งประมวลผลภายใน Tags ได้อีกด้วยเช่น

```javascript
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

การเรียก function ภายใน Tags JSX ก็สามารถทำได้เช่น

```javascript
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

สำหรับการใส่ค่า Attribute ใน Tags สามารถทำได้เหมือน html เช่น

```javascript
const element = <div tabIndex="0"></div>;
```

แต่ใน ReactJS นั้นได้แนะนำให้ใช้ `{}` ในการให้ค่ากับ Attribute ดังตัวอย่าง

```javascript
const element = <img src={user.avatarUrl}></img>;
```

หาก Tags นั้นไม่มีค่า หรือ Tags ซ้อนอยู่ภายในก็สามารถย่อการเขียนโด้ดได้ด้วยการปิด Tags ด้วย `/>`

```javascript
const element = <img src={user.avatarUrl}/>;
```

### Reference
[https://reactjs.org/docs/introducing-jsx.html](https://reactjs.org/docs/introducing-jsx.html)
