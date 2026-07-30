- [Variable](#variable)
  - [let](#let)
  - [Generic (type động)](#generic-type-động)
- [Array](#array)
- [function](#function)
  - [Arrow function](#arrow-function)
- [Object](#object)
- [type](#type)
---
# Variable
## let
**Ex**
```ts
let age: number = 25
let name: string = "Thang"
let isAdmin: boolean = true
```
## Generic (type động)
**Ex**
```ts
function identity<T>(value: T): T {
  return value
}

identity<string>("hello")
identity<number>(123)
```
**Ex2: Generic với array**
```ts
function getFirst<T>(arr: T[]): T {
  return arr[0]
}
```
# Array
**Ex**
```ts
// JS
const numbers = [1,2,3]

// TS
const numbers: number[] = [1,2,3] // const numbers: Array<number> = [1,2,3]
```
**Ex: Cho phép nhiều type**
```ts
let id: number | string

id = 1
id = "abc"
```
**Ex**
```ts
let value: unknown

if (typeof value === "string") {
  console.log(value.toUpperCase())
}
```
# function
**Ex**
```ts
//  hàm js thường
function add(a, b) {
  return a + b
}

// hàm ts
function add(a: number, b: number): number {
  return a + b
}
```
**Ex: default param**
```ts
function greet(name: string = "guest") {
  return "Hello " + name
}
```
## Arrow function
**Ex**
```ts
const sum = (a: number, b: number): number => {
  return a + b
}
```
# Object
**Ex: inline type**
```ts
const user: {
  id: number
  name: string
} = {
  id: 1,
  name: "Thang"
}
```
**Ex2: type alias**
```ts
type User = {
  id: number
  name: string
}

const user: User = {
  id: 1,
  name: "Thang"
}
```
**Ex: Interface (rất phổ biến)** 
```ts
interface User {
  id: number
  name: string
}

// interface User {
//   id: number
//   name: string
//   email?: string
// }
```
**Ex: Extend**
```ts
interface Admin extends User {
  role: string
}
```
# type
```bash
type là:
  Một cách đặt tên cho một kiểu dữ liệu để dùng lại nhiều lần.
```
**Không dùng type**
```js
let user: {  name: string;  age: number;}; // một người dùng

// Nếu có nhiều biến:
let user1: {  name: string;  age: number;};
let user2: {  name: string;  age: number;};
let user3: {  name: string;  age: number;};
// Rất dài và lặp lại.
```
**Dùng type**
```js
type User = {  name: string;  age: number;};

// Bây giờ:
let user1: User;
let user2: User;
let user3: User;
// Dễ đọc hơn nhiều.
```
**Ex1: Ví dụ thực tế**
```python
type User = {  name: string;  age: number;};
const user: User = {  name: "Thắng",  age: 25,};

# Nếu thiếu trường:
const user: User = {  name: "Thắng",};
# TypeScript báo lỗi:
# Property 'age' is missing
```
**Ex2: Type cho hàm**
```js
function add(a: number, b: number): number {  return a + b;}

// Có thể tạo type:
type AddFunction = (  a: number,  b: number) => number;
// Sử dụng:
const add: AddFunction = (a, b) => {  return a + b;};
```
**Ex3: Type cho mảng**
```js
type User = {  name: string;  age: number;};

// Danh sách người dùng:
const users: User[] = [  {    name: "An",    age: 20,  },  {    name: "Bình",    age: 22,  },];
```
**Union Type: Cho phép nhiều kiểu dữ liệu**
```js
type Id = string | number; 

// Hợp lệ:
let id: Id = 123;
id = "abc";

// Không hợp lệ:
id = true;
```
**Ex**
```js
type Status =  | "loading"  | "success"  | "error";
let status: Status;status = "loading"; // OKstatus = "success"; // OKstatus = "abc";     // Lỗi
```