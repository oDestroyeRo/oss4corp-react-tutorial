# Tools for ReactJS Developer
***

## Node.js
Node.js คือ platform การเขียนโปรแกรมด้วย JavaScript ที่ฝั่ง server

## npm
npm นั้นเป็นโปรแกรมถูกติดตั้งมาพร้อมกับ Node.js เพื่อทำหน้าที่จัดการ package เสริมต่างๆ ไม่ว่าจะเป็นการติดตั้ง application หรือการติดตั้ง module ต่างๆ ที่เป็น dependency ของ application เพียงแค่เราระบุชื่อ package ที่ต้องการจะใช้ มันก็จะไปตรวจสอบชื่อ package นั้นใน registry เมื่อพบแล้ว มันก็จะดาวน์โหลด package นั้นๆ มาให้เรา

เราสามารถดาวน์โหลดและติดตั้ง Node.js ได้ที่ [https://nodejs.org/en/](https://nodejs.org/en/)

เมื่อติดตั้งเรียบร้อยแล้ว เราสามารถทดการติดตั้ง Node.js ไว้หรือยังด้วย command line

```
node -v
```
npm จะถูกติดตั้งพร้อมกับ Node.js โดยสามารถทดสอบด้วยคำสั่ง

```
npm -v
```

เมื่อลง `npm` เรียบร้อยแล้วเราจะสมารถลง package ต่างๆได้ด้วยคำสั่ง

```
npm install <package_name>
```

หรือ

```
npm -i <package_name>
```

ทั้งนี้ `npm install` ยังมี option เพิ่มเติมที่พบได้บ่อยครั้งเช่น

```
npm install <package_name> --save
```

โดย option `--save` จะช่วยในการอับเดท package ที่เกี่ยวข้อง

`npm` ยังมีคำสั่งอื่นๆอีกมากมาย แต่ที่พบเห็นได้บ่อยได้แก่ `npm install` และ `npm update` โดยรายละเอียดของคำสั่งนี้จะพบได้ในส่วนต่อไป

*คำสั่ง npm นั้นจำเป็นต้องใช้ internet ในการเช็คและดาวน์โหลด


## creact-react-app

`create-react-app` เป็น tools ที่ช่วยสร้าง react project ใหม่ สามารถลงได้ด้วยคำสั่ง

```
npm install create-react-app
```

หากติดตั้งสำเร็จแล้ว เราจะสามารถใช้คำสั่ง `create-react-app` ใน command line ได้เลย

ตัวอย่างการสร้างโปรเจคใหม่

```
create-react-app my-first-app
```

จากตัวอย่างเราจะพบ folder `my-first-app` ที่ถูกสร้างขึ้นมาใหม่ โดยใน folder จะประกอบด้วย

```
- README.md
- package.json -> เป็นไฟล์ที่แสดงรายละเอียดของ package ที่ใช้ใน project
- package-lock.json
- node_modules -> เป็น folder เก็บ source code ของ package ที่เราลงด้วยคำสั่ง npm install
- public -> เป็น folder เก็บ static file, เช่น index.html, image file, logo icon, ...etc
- src -> เป็น folder เก็บไฟล์ javascript
```

***Tip** ในกรณีที่ต้องการ copy project ไปยังเครื่องอื่น สามารถทำได้โดย copy `package.json`, `public`, `src` เท่านั้นเพราะ `package.json` ได้ระบุรายละเอียดของ package ที่จำเป็นในโปรเจคอยู่แล้ว ซึ่งสามารถลงได้ด้วยคำสั่ง `npm install`


เราสามารถรันโปรเจคเพื่อทดสอบด้วยคำสั่ง `npm run start`


