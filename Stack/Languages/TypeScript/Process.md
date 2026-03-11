- [Variable](#variable)
  - [let](#let)
  - [Generic (type động)](#generic-type-động)
- [Array](#array)
- [function](#function)
  - [Arrow function](#arrow-function)
- [Object](#object)
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