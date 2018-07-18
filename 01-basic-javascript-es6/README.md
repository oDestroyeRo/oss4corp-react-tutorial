#Basic Javascript, Javascript ES6
***
##Const and Let

การประกาศตัวแปรใน Javascript

```javascript
var name = "OSS4CORP";
```

สิ่งที่เพิ่มเข้ามาใน ES6

```javascript
const name = "OSS4CORP";
let hostby = "Kasetsart University";
```

`const` ใช้กับสิ่งที่ไม่เปลี่ยนแปลงเช่น สระในภาษาอังกฤษ

```javascript
const vowels = ["a", "e", "i", "o", "u"];  
```

`let` เป็นการประกาศตัวแปรเช่นเดียวกับ `var` แต่จะต่างกันที่ขอบเขตในการใช้งาน โดยตัวแปรที่ประกาศด้วย ```let``` จะมีขอบเขตการใช้งานแบบ local เท่านั้น เช่น


```javascript
function getTodayClass() {  
  if(1 == 1){
    let local = 'ReactJS'
  }
  return local;
}
getTodayClass();
//return 'local' is undefined
```

หาเปลี่ยนการประกาศตัวแปรจาก `let` ไปเป็น `var`

```javascript
function getTodayClass() {  
  if(1 == 1){
    var local = 'ReactJS'
  }
  return local;
}
getTodayClass();
//return 'ReactJS'
```
###การใช้ตัวแปรแบบ JSON
การประกาศตัวแปรแบบ JSON (JavaScript Object Notation)

```
function getTodayClassName() {
	let todayClass = {name: 'ReactJS', hostby: 'ComSci KU'};
	return todayClass.name;
}
getTodayClassName();
//return 'ReactJS'
```

<mark>Tip</mark> เราสามารถดึงค่าจากตัวแปรประเภท JSON ได้ด้วย `=`

```
function getTodayClassName() {
	let todayClass = {name: 'ReactJS', hostby: 'ComSci KU'};
	let {name} = todayClass;
	return name;
}
getTodayClassName();
//return 'ReactJS'
```


***
##Rest and Spread Operator
