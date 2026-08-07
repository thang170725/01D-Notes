- [JSON.parse() (Để chuyển một chuỗi JSON thành một đối tượng Javascript)](#jsonparse-để-chuyển-một-chuỗi-json-thành-một-đối-tượng-javascript)
---
# JSON.parse() (Để chuyển một chuỗi JSON thành một đối tượng Javascript)
```js
function main(){
   let json = `{"employees": [
      {"firstName": "John", "lastName": "Doe"},
      {"firstName": "Anna", "lastName": "Smith"},
      {"firstName": "Peter", "lastName": "Jones"}
   ]}`;
   console.log(typeof json);
   let data = JSON.parse(json);
   console.log(data.employees[0]);
}
main()
String
{ firstName: 'John', lastName: 'Doe' }
```