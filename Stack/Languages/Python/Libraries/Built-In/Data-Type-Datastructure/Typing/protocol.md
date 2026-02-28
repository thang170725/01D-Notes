# Protocol
**Ex**
```python
# 1. Định nghĩa "interface" bằng Protocol
class Speaker(Protocol):
    def speak(self) -> str:
        ...

# 2. Các class KHÔNG cần kế thừa Speaker
class Dog:
    def speak(self) -> str:
        return "Gâu gâu"

class Human:
    def speak(self) -> str:
        return "Hello"

class Robot:
    def speak(self) -> str:
        return "Beep beep"

# 3. Class KHÔNG đúng interface
class Cat:
    def meow(self) -> str:
        return "Meo meo"

# 4. Hàm dùng duck typing
def make_sound(x: Speaker) -> None:
    print(x.speak())

if __name__ == "__main__":
    make_sound(Dog())
    make_sound(Human())
    make_sound(Robot())
    make_sound(Cat())
```
**Ex2**
```python
from typing import Protocol

class Information(Protocol):
    def information():
        pass

class Student:
    def __init__(self, gpa):
        self.gpa = gpa
        
    def information(self):
        if self.gpa > 3.2:
            return "Được khen thưởng"
        else:
            return "Không được khen"

class Teacher:
    def __init__(self, research):
        self.research = research
        
    def information(self):
        if self.research >= 2 :
            return "Được khen thưởng"
        else:
            return "Không được khen"

class Manager:
    def __init__(self):
        ...
    def information(self):
        return "được khen thưởng"

def main_information(obj : Information):
    print(obj.information())  

s = Student(3.2)
t = Teacher(3)
m = Manager()

main_information(s)
main_information(t)
main_information(m)
```