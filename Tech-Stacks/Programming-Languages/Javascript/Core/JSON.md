JS JSON (Javascript Object Notation)
Xem ví dụ ở đây: https://www.w3schools.com/js/js_json.asp
JSON là một loại định dạng và vận chuyển dữ liệu. Thường được sử dụng khi dữ liệu được gửi tử máy chủ đến trang web.
Định dạng của JSON là văn bản (String).
JSON.parse()
Để chuyển một chuỗi JSON thành một đối tượng Javascript.
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