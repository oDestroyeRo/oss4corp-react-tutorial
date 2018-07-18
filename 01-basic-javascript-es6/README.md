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

##การใช้ตัวแปรแบบ JSON
การประกาศตัวแปรแบบ JSON (JavaScript Object Notation)

```javascript
function getTodayClassName() {
	let todayClass = {name: 'ReactJS', hostby: 'ComSci KU'};
	return todayClass.name;
}
getTodayClassName();
//return 'ReactJS'
```

*เราสามารถดึงค่าจากตัวแปรประเภท Object ได้ด้วย `=` โดย Object จะมีโครงสร้างเหมือน JSON

```javascript
function getTodayClassName() {
	let todayClass = {name: 'ReactJS', hostby: 'ComSci KU'};
	let {name} = todayClass;
	return name;
}
getTodayClassName();
//return 'ReactJS'
```

source [https://coursework.vschool.io/es6-basics/#restandspreadoperator]