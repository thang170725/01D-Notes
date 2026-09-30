- [@override (ghi đè viết lại phương thức của class cha)](#override-ghi-đè-viết-lại-phương-thức-của-class-cha)
- [toString](#tostring)
---
# @override (ghi đè viết lại phương thức của class cha)
```bash
override thuộc java core
```
**Ex**
```java
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Gâu gâu");
    }
}

// override = ghi đè/viết lại phương thức của class cha.
```
# toString
**Ex: Quản lý danh sách sinh viên**
```java
class student{
	String name, room, sex;
	student(String name, String room, String sex){
		this.name = name;
		this.room = room;
		this.sex = sex;
	}
	@Override
	public String toString() {
		return "student [name=" + name + ", room=" + room + ", sex=" + sex + "]";
	}
}
public class Solution{
	public static void main(String[] args) {
		student [] list = new student[2];
		student sv1 = new student("JSON", "12A1", "male");
		student sv2 = new student("MICK", "12A1", "female");
		list[0] = sv1;
		list[1] = sv2;
		for (student student : list) {
			System.out.println(student);
		}
	}
}
// student [name=JSON, room=12A1, sex=male]
// student [name=MICK, room=12A1, sex=female]
```