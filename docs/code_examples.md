# Learning OOP

**I m learning OOP and making notes of it as i go (reference:[ Corey Schafer](https://youtube.com/playlist?list=PL-osiE80TeTsqhIuOqKhwlXsIBIdSeYtc&si=WBUQBxK8mvtON8cT))** But i have did my own research too and made it as detailed as possible.

__Why is OOP needed?__:  
OOP logically helps us to group data and functions such that it is easy to use and build upon if need be.Everything is an object even integers,lists,etc are all objects.
```py
class Employee:
    pass
INTEGER = 1
emp_1 = Employee()
emp_2 = Employee()
print(emp_1)
print(emp_2)
print(type(INTEGER))
```

```
<__main__.Employee object at 0x000002AB96A64D10>
<__main__.Employee object at 0x000002AB96A64F50>
<class 'int'>
```

`emp_1` is an instance variable, each instance variable contains data unique to itself.

### What are attributes and methods?
in simple words attributes are properties of an object, for example if cat is an object the colour of the cat is an attribute.  
And methods are functions inside a class they represent what an object can do, for example a cat can jump is a method.

We can make attributes inside the class's code block or we can assign them directly like below, this is called dynamic attribute assignment:
```py
class Employee:
    pass
emp_1 = Employee()
emp_2 = Employee()
emp_1.first = "corey"
emp_2.first = "Rai"
print(emp_1.first)
print(emp_2.first)
```
This attribute is only available to that instance and not to the class.It gets assigned when that line of the code gets executed.

### The init method
```py
class Employee:
    def __init__(self,fname,lname,pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
    def work(self):
        print(f"working...")
emp_1 = Employee("corey","schafer",5000)
emp_2 = Employee("Rai","Rai",6000)
print(emp_1.email)
emp_1.work()#method being used
```
Here the init method is used to create attributes for the object Employee and is common to all the instances unlike the dynamic attribute assignment.Also the self represents the instance, The self can be anything that represents the instance but mostly "self" is used.init method name is surrounded by `__` (2 underscores) these are called dunders and we will learn about them later.  

`self.fname = fname` saves the value of `fname` inside the object so each instance can have its own `fname` and it stays  
as an attribute to the object.
`Employee("corey", "schafer", 5000)` calls `Employee.__init__`(this is how methods are used with the object)
Python secretly does this:
```py
Employee.__init__(emp_1, "corey", "schafer", 5000)
```
self refers to emp_1 inside the class and rest are attributes so its not necessary to use self when calling the class.

### Methods (in more detail)
```py
class Employee:
    def __init__(self,fname,lname,pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
    def fullname(self):
        return ("{} {}".format(self.fname, self.lname))
emp_1 = Employee("corey","schafer",5000)
emp_2 = Employee("Rai","Rai",6000)
print(emp_1.fullname())
```
Previously we saw `work` method but we haven't spoken in detail about it,here we creating a method to return
fullname of the person.We are doing so by calling it with the instance `emp_1.fullname()` which then gets
printed.As mentioned before `__init__` is also a method except except the self is the instance itself and 
doesn't need to be explicitly passed.
When we call `emp_1.fullname()` python secretly does `Employee.fullname(emp)` so a self is necessary if it is
an instance method.What is an instance method, for now we would simply say a method defined inside a class is an instance method.
But there are other methods like static methods and class methods which will be learned later.
if you dont use self in the fullname that is `def fullname():` it will give a TypeError
```py
Exception has occurred: TypeError
Employee.fullname() takes 0 positional arguments but 1 was given
  File "C:\Users\hp\Desktop\White room\Python\python essentials\coding-journal-2025\oop\test.py", line 12, in <module>
    print(emp_1.fullname())
          ^^^^^^^^^^^^^^^^
TypeError: Employee.fullname() takes 0 positional arguments but 1 was given
```  
You can also do `Employee.fullname(emp)` instead of `emp_1.fullname()` and the difference is method is getting called on the class
and the instance has to be explicitly passed whereas `emp_1.fullname()` the method is directly being used on the instance









