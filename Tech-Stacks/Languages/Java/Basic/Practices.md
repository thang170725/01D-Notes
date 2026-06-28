# Thiết lập chương trình đầu tiên
```bash
src
 └── microservice_demo
      └── order_service
           └── Test.java
```
```java
package microservice_demo.order_service;

public class Test { // phải trùng tên với file tạo (Test.java)
    public static void main(String[] args) {
        System.out.println("hello world");
    }
}

// javac microservice_demo/order_service/Test.java
// java microservice_demo.order_service.Test
```