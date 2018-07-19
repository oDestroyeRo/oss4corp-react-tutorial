#Basic Javascript, ES6
***
ES6 ย่อมาจาก ECMAScript 6 เป็นมาตรฐานของภาษา JavaScript เริ่มใช้งานเมื่อปี 2015
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

***
##Rest and Spread Operator
Rest Parameter เป็นวิธีเขียนฟังก์ชันโดยรวม parameter ให้เป็น Array ก้อนเดียว

```javascript
function sum (...numbers) {
  let sum = 0;
  for(let i=0; i<numbers.length; i++) {
    sum += numbers[i];
  }
  return sum;
}
sum(1, 2, 3, 4, 5);
//return 15
```
Spread Operator เป็นการแจกแจงตัวแปรที่เป็น Array หรือ Object ตัวอย่างการใช้งานเช่น โดยปกติแล้วเราสามารถรวมตัวแปร Array ด้วย `.concat`

```javascript
const landAnimals = ['dog', 'cat'];
const aquaticAnimals = ['fish', 'squid', 'crab'];  
const animals = landAnimals.concat(aquaticAnimals);

console.log(animals);// ["dog", "cat", "fish", "squid", "crab"]
```

เราสามารถเขียนโค้ดโดยใช้ Spread Operator ดังนี้

```javascript
const landAnimals = ['dog', 'cat'];
const aquaticAnimals = ['fish', 'squid', 'crab'];  
const animals = [...landAnimals, ...aquaticAnimals];

console.log(animals);// ["dog", "cat", "fish", "squid", "crab"]
```

โดยการใช้ Spread Operator จะช่วยลดจำนวนโค้ดของเราได้เช่น เมื่อต้องการ `.concat` Array มากกว่า 2 ชุด

```javascript
const animals = [...landAnimals, ...aquaticAnimals, ...otherAnimal];
```

นอกจากนี้ Spread Operator ยังสามารถเพิ่มตัวแปรแบบปกติได้ด้วย เช่น

```javascript
const animals = ["monkey", "lobster", ...landAnimals, ...aquaticAnimals, ...otherAnimal];
```

ตัวอย่างการใช้งานอื่นๆ เช่น การทำ Validator

```javascript
function validateShoppingList(...items) {  
  if (items.indexOf('milk') < 0) {
    return [ 'milk', ...items ];
  }

  return items;
}
console.log(validateShoppingList('oranges', 'bread', 'eggs'));
//['milk', 'oranges', 'bread', 'eggs']
```

***
##Default Parameters
การเรียก javascript function นั้นไม่จำเป็นต้องส่ง parameter ให้ครบทุกตัวก็สามารถทำงานได้ แต่โค้ดใน function นั้นๆ ต้องมีการตรวจเช็คค่าก่อนทุกครั้งเพื่อป้องกัน error

การเขียน function แบบเดิม

```javascript
function calculateSquareInches(width, length, thickness){  
	if (thickness === undefined){
		thickness = 1;
	}
	return width * length * thickness;
}
```

จะเห็นได้ว่าเราต้องเช็คค่า `thickness` ก่อนว่ามีการส่งค่ามาหรือไม่ หากไม่มีการส่ง `thickness` มาก็ทำการตั้งให้ `thickness` มีค่าเท่ากับ 1 เพื่อคำนวณหาผลลัพธ์ต่อไป ( * คำอธิบายเกี่ยวกับ operation `===` จะอยู่ในช่วงท้ายของหัวข้อนี้)

เราสามารถเปลี่ยนโค้ดใหม่โดยตั้ง Default Parameters ดังนี้

```javascript
function calculateSquareInches(width, length, thickness = 1){  
    return width * length * thickness;
}
```

จะเห็นได้ว่าโค้ดรูปแบบใหม่จะมีจำนวนบรรทัดที่น้อยกว่า แต่ยังให้ผลลัพธ์เหมือนเดิม

***
##Template Literals
การจัด format ของ string ใน Javascript นั้นสามารถทำได้ด้วยคำสั่ง `+` เช่น

```javascript
let name = 'ReactJS';
let hostby = 'Comsci KU';  
console.log('Hi today course is ' + name + ', host by ' + hostby);
//"Hi today course is ReactJS, host by Comsci KU"
```

เมื่อมีการเชือมต่อตัวแปรหลายๆตัว จะทำให้โค้ดดูยากขึ้น โดย ES6 ได้ออกแบบการเขียนโค้ดส่วนนี้ใหม่ ดังตัวอย่าง

```javascript
let name = 'ReactJS';
let hostby = 'Comsci KU';

console.log(`Hi today course is ${name}, host by ${hostby}`);
//"Hi today course is ReactJS, host by Comsci KU"
```
โดยการเขียนโด้ดแบบใหม่ยังสามารถรองรับคำสั่งต่างๆภายใน Template Literals ได้อีกด้วยเช่น

***
##Object Literals
Object literal syntax เป็นวิธีการเขียนโค้ดแบบใหม่ให้ดูเรียบร้อยขึ้น สำหรับความแตกต่างของ javasript แบบเก่า กับ ES6 สามารถดูตัวอย่างได้ดังนี้

การสร้างตัวแปรแบบ Object แบบเดิม

```javascript
const red = '#ff0000';  
const blue = '#0000ff';

const COLORS = { red: red, blue: blue };  
```

โดยแบบ ES6 จะสามารถเขียนโด้ดได้ดังนี้

```javascript
const red = '#ff0000';  
const blue = '#0000ff';
const COLORS = { red, blue };  
```

แบบเดิม

```javascript
const fields = ['firstName', 'lastName', 'phoneNumber'];

const props = { fields: fields };  
```

สร้างเขียนแบบใหม่ได้ดังนี้

```javascript
const fields = ['firstName', 'lastName', 'phoneNumber'];
const props = { fields };  
```

การเขียน function หรือประกาศตัวแปรเป็น function แบบเดิม

```javascript
function canvasDimensions(width, initialHeight) {  
  const height = initialHeight * 9 /16;
  return {
    width: width,
    height: height
  };
}
```
หรือ

```javascript
const canvasDimensions = function(width, initialHeight) {  
  const height = initialHeight * 9 /16;
  return {
    width: width,
    height: height
  };
}
```

แบบใหม่ไม่จำเป็นต้องมีเขียน function กำกับ

```javascript
const canvasDimensions = (width, initialHeight) => {  
  const height = initialHeight * 9 /16;
  return {
    width,
    height
  };
}
```

การสร้าง​ Object และ Method ไม่จำเป็นต้องขึ้นต้นด้วย function

```javascript
const color = 'red';

const Car = {  
  color: color,
  drive: function() {
    return 'Vroom!';
  },
  getColor: function() {
    return this.color;
  }
};
```

สร้างเขียนแบบใหม่ได้ดังนี้

```javascript
const color = 'red';

const Car = {  
  color,
  drive() {
    return 'Vroom!';
  },
  getColor() {
    return this.color;
  }
};
```

***
##Destructuring
การเขียนโด้ดแบบ ES6 นั้นทำให้การเขียนโด้ด javascript เปลี่ยนไปและทำให้โค้ดดูสะอาดและลดจำนวนบรรทัดได้ ตัวอย่างเช่น

การดึงค่าจาก object

```javascript
var expense = {  
  type: "Business",
  amount: "$45 USD"
};

```

เมื่อเราต้องการค่าจาก expense

```javascript
var type = expense.type;  
var amount = expense.amount;
```

จะเห็นได้ว่าโด้ดจะต้องอ้างอิงถึง object และค่าของมันทุกครั้ง เราสามารถลดโด้ดได้ดังนี้

```javascript
const {type} = expense;  
const {amount} = expense;  
```

หรือ

```javascript
const { type, amount } = expense;  
```

หาก object ไม่มีค่าของที่เราระบุ ตัวแปรที่สร้างใหม่จะมีค่าเท่ากับ `undefined` เช่น

```javascript
const { type, amount, ext } = expense;  
//ext = undefined
```

ตัวอย่างการดึงค่าแรกจากตัวแปร Array

```javascript
const firstVegetable = vegetables[0];  
```

เราสามารถเขียนโค้ดใหม่ได้ดังนี้

```javascript
const [ firstVegetable ] = vegetables  
```

หรือหาต้องการค่าแรก และค่าที่สองจากตัวแปร Array

```javascript
const [ firstVegetable, secondVegetable ] = vegetables  
```

การดึงค่าแบบใหม่นี้สามารถใช้ร่วมกันระหว่าง Array และ object ได้ดังตัวอย่างต่อไปนี้

```javascript
const people = [
  {name: 'Bob', age: 31},
  {name: 'Joe', age: 29},
  {name: 'Ben', age: 42}
];
const [{ name }] = people
//name = 'Bob'
```

###map function
`map` เป็นคำสั่งใหม่​(method ของ Array)ที่สามารถใช้แทนการเขียน forloop แบบเดิม ตัวอย่างต่อไปจะแสดงถึงการใช้ `map`

เมื่อเรามีตัวแปรเป็น Array 2 มิติดังนี้

```javascript
const points = [  
  [4, 5],
  [10, 1],
  [0, 40]
];
```
หากเราต้องการนำค่า `points` ไปวาดกราฟด้วย Library อื่นๆโดยมากแล้วเราจำเป็นต้องแปลงค่าของ Array ให้อยู่ในรูปดังตัวอย่าง

```javascript
[
  { x: 4, y: 5 },
  { x: 10, y: 1 },
  { x: 0, y: 40 }
]
```

```javascript
let new_points = [];
for(let i=0; i<points.length; i++){
  new_points.push({x: points[0], y:points[1]})
}
```

หากเราใช้ `map` ในการสร้างตัวแปร `new_point` จะสามารถทำได้หลายวิธีดังตัวอย่างที่จะแสดงต่อไป

```javascript
let new_points = points.map(point => {  
  const x = point[0];
  const y = point[1];
});
```

```javascript
let new_points = points.map(point => {  
  const [ x, y ] = point;
});
```

```javascript
let new_points = points.map(([ x, y ]) => {  
  return { x: x, y: y };
});
```

```javascript
let new_points = points.map(([ x, y ]) => {  
  return { x, y };
});
```


***
##Arrow Functions
Arrow functions เป็น syntax ในการเขียน function แบบใหม่เพื่อให้โด้ดดูสะอาดขึ้น 

ตัวอย่างการเขียน function แบบปกติ

```javascript
function add(a, b) {
	return a+b;
}
```
หรือ

```javascript
const add = function(a, b){  
    return a + b;
}
```
ด้วย Arrow functions เราสามารถเขียนโด้ดโดยใช้ `=>` แทนดังนี้

```javascript
const add = (a, b) => {  
    return a + b;
}
```

โดยใน `=>{...}` จะเป็นรายละเอียดของ function, หาก function มีการทำงานเพียงบรรทัดเดียว เราสามารถย่อโค้ดได้อีกดังนี้

```javascript
const add = (a, b) => a + b;  
```

หาก parameter ที่จะส่งไปยัง function มีเพียงตัวเดียวเราสามารดละ () ได้เช่น

```javascript
const double = (num) => num * 2;  
```

สามารถเขียนย่อได้ดังนี้

```javascript
const double = num => num * 2;  
```

หากต้องการสร้าง function ที่ไม่มี parameter สามารถใช้ `()` แทนดังนี้

```javascript
const logHello = () => console.log("hello");  
```

ตัวอย่างการเขียนโด้ดด้วย `map`

```javascript
const numbers = [1, 2, 3]
const result = numbers.map(function(number) {  
    return 2 * number;
});
//result = [2, 4, 6]
```

สามารถใช้ Arrow function ได้โดยจะเขียนโค้ดดังนี้

```javascript
const numbers = [1, 2, 3]
const result = numbers.map(number => 2 * number);  
//result = [2, 4, 6]
```

***
#Promise



###Reference
- Part of this document is translate from [https://coursework.vschool.io/es6-basics/ link] (https://coursework.vschool.io/es6-basics/)
