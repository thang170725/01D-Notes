from abc import ABC, abstractmethod

class Animal(ABC):

    def sleep(self):
        print("Zzz...")

    @abstractmethod
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Gâu gâu"

class Cat(Animal):
    pass

c = Cat()  # TypeError: Can't instantiate abstract class
