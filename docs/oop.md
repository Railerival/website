# Learning OOP

### About the page
**I m learning OOP and making notes of it as i go (reference:[ Corey Schafer](https://youtube.com/playlist?list=PL-osiE80TeTsqhIuOqKhwlXsIBIdSeYtc&si=WBUQBxK8mvtON8cT))** But i have did my own research too and made it as detailed as possible.
I need to re-check the last topic for issues and add a few more stuff.

__Why is OOP needed?__:  
OOP logically helps us to group data and functions such that it is easy to use and build upon if need be.Everything is an object even integers,lists,etc.
```py
class Employee:
    pass
INTEGER = 1
emp_1 = Employee() #instantiation or basically creating instances 
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
`Whats an instance?`: It is an object created using the blueprint(class),  
`Whats instantiation?`: It is creation of the instance   
`emp_1` is an instance variable, each instance variable generally contains data unique to itself.


### What are attributes and methods?
In simple words attributes are properties of an object, for example if cat is an object the colour of the cat is an attribute.   
Methods are functions inside a class they represent what an object can do, for example a cat can jump is a method.  
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
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
    def work(self):
        print("working...")
emp_1 = Employee("corey", "schafer", 5000)
emp_2 = Employee("Rai", "Rai", 6000)
print(emp_1.email)
emp_1.work() #method being used
```
Here the init method is used to create attributes for the object Employee and the attribute is common to all the instances unlike the dynamic attribute assignment, but still the data of the attributes might vary for different instances.Also the `self` represents the instance, The self can be replaced with anything that represents the instance but mostly "self" is used. init method name is surrounded by `__` (2 underscores) these are called dunders and we will learn about them later.  

`self.fname = fname` saves the value of `fname` inside the object so each instance can have its own `fname` and it stays as an attribute to the object.But if it was not saved inside the object it would be forgotten next time the instance is used.   
`Employee("corey", "schafer", 5000)` calls `Employee.__init__` implicitly(this is how methods are used with the object).  
Python secretly does this:`Employee.__init__(emp_1, "corey", "schafer", 5000)` self refers to emp_1 inside the class and rest are attributes so its not necessary to use self when calling the class.

### Methods (in more detail)
```py
class Employee:
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
    def fullname(self):
        return ("{} {}".format(self.fname, self.lname))
emp_1 = Employee("corey", "schafer", 5000)
emp_2 = Employee("Rai", "Rai", 6000)
print(emp_1.fullname())
```
Previously we saw `work` method but we haven't spoken in detail about it,here we are creating a method to return fullname of the person.We are doing so by calling it with the instance `emp_1.fullname()` which then gets
printed.As mentioned before `__init__` is also a method except the self is the instance itself and 
doesn't need to be explicitly passed.
When we call `emp_1.fullname()` python secretly does `Employee.fullname(emp_1)` so a self is necessary as an argument if it is an instance method.What is an instance method, for now we would simply say a method defined inside a class is an instance method.
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
You can also do `Employee.fullname(emp_1)` instead of `emp_1.fullname()` and the difference is method is getting called on the class
and the instance has to be explicitly passed whereas `emp_1.fullname()` the method is directly being used on the instance

### Class variables
Variables that are shared among all the instances of the class.
```py
class Employee:
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
    def applyraise(self):
        self.pay = self.pay*1.04
emp_1 = Employee("corey", "schafer", 5000)
emp_2 = Employee("Rai", "Rai", 6000)
print(emp_1.pay)
emp_1.applyraise()
print(emp_1.pay)
```
This works but a better way would be:
```py
class Employee:
    raise_ = 1.04
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
    def applyraise(self):
        self.pay = self.pay*self.raise_
emp_1 = Employee("corey", "schafer", 5000)
emp_2 = Employee("Rai", "Rai", 6000)
print(emp_1.pay) #prints the pay
emp_1.applyraise() #applies the raise
print(emp_1.pay) #prints the new pay
print(Employee.raise_) #prints the class variable raise_
print(emp_1.raise_) #raises emp_1's salary
print(emp_2.raise_) #raises emp_2's salary
print(emp_1.__dict__) 
print()
print(Employee.__dict__)
```
the last 3 prints give some info:
```
{'fname': 'corey', 'lname': 'schafer', 'pay': 5200.0, 'email': 'coreyschafer@gmail.com'}

{'__module__': '__main__', '__firstlineno__': 1, 'raise_': 1.04, '__init__': <function Employee.__init__ at 0x7f0b38452fb0>, 'applyraise': <function Employee.applyraise at 0x7f0b38453060>, '__static_attributes__': ('email', 'fname', 'lname', 'pay'), '__dict__': <attribute '__dict__' of 'Employee' objects>, '__weakref__': <attribute '__weakref__' of 'Employee' objects>, '__doc__': None}
```
Here there is a class variable which is an attribute of the class and is also a common attribute to all the instances.
In this line `self.pay = self.pay*self.raise`, `self.raise` was used instead of using `raise` as the variable because it would not be accessible if `self` is not used, another way to access it would be `self.pay = self.pay*Employee.raise`.
```py
print(Employee.raise_)
print(emp_1.raise_)
print(emp_2.raise_)
```
This tells how the class variable can be accessed outside the class and shows that it is common to all instances and
the class itself.
```py
print(emp_1.__dict__)
print(Employee.__dict__)
```
This prints the namespace of the instance and the class and shows that the `print(Employee.__dict__)` one displays the class variable but the `print(emp_1.__dict__)` one does not have it.But when we do the `print(emp_1.raise_)` the instance accesses it from the 
class.
```py
class Employee:
    raise_ = 1.04
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
emp_1 = Employee("corey", "schafer", 5000)
emp_2 = Employee("Rai", "Rai", 6000)
Employee.raise_ = 1.05
print(Employee.raise_)
print(emp_1.raise_)
print(emp_2.raise_)
```
`Employee.raise_ = 1.05` changed the class variable for everything including the instances and the class
```py
class Employee:
    raise_ = 1.04
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
emp_1 = Employee("corey", "schafer", 5000)
emp_2 = Employee("Rai", "Rai", 6000)
emp_1.raise_ = 1.05
print(Employee.raise_)
print(emp_1.raise_)
print(emp_2.raise_)
print(emp_1.__dict__)
```
`emp_1.raise_ = 1.05` gives a variable attribute to only emp_1 instance and its also seen its namespace.And it doesnt change it for the class or the other instances....

```py
class Employee:
    no_of_employees = 0
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
        Employee.no_of_employees += 1
emp_1 = Employee("corey", "schafer", 5000)
emp_2 = Employee("Rai", "Rai", 6000)
print(Employee.no_of_employees)
```
This gives an output 2 because the variable gets incremented 2 times because 2 instances were instantiated
and would get stored in the memory as a class variable

but make sure u dont do this instead:
```py
class Employee:
    no_of_employees = 0
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
        self.no_of_employees += 1
emp_1 = Employee("corey", "schafer", 5000)
emp_2 = Employee("Rai", "Rai", 6000)
print(Employee.no_of_employees)
```
the first one increments it for the class which increments it for all the instances commonly but the second one only increments it for the class.
### Class methods and Static methods 

```py
class Employee:
    raise_ = 1.04
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
    @classmethod
    def set_raise_amount(cls, amount):
        cls.raise_ = amount
emp_1 = Employee("corey", "schafer", 5000)
emp_2 = Employee("Rai", "Rai", 6000)
Employee.set_raise_amount(1.05)
```
This is a class method example, here a decorator `@classmethod` is used and instead of the instance `self` the class is used in the form of `cls`.  
Even if we use `emp_1.set_raise_amount(1.05)` instead that would still
alter the class variable for all the instances.

### Alternative constructors using Class methods
Instead of instantiating the class manually what if we were given a string and then we have to somehow parse it,before instantianting instances? We can do that using class methods too
and this is what alternative constructors mean.

```py
class Employee:
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
    @classmethod
    def from_string(cls, emp_str):
        first, last, pay = emp_str.split("-")
        return cls(first, last, pay)
emp_str_1 = "John-Doe-70000"
emp_1 = Employee("corey", "schafer", 5000)
emp_2 = Employee("Rai", "Rai", 6000)
new_emp_1 = Employee.from_string(emp_str_1)
print(new_emp_1.pay)
```
This is how class methods are used to create instances, Here to parse the data, a class method is used which was named `from_string` mostly such functions who are used to instantiate instances from a data have conventionally their name starting with `from`.

### Static methods

```py
class Employee:
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
    @staticmethod
    def is_workday(day):
        day = day.lower
        if day == "saturday" or day == "sunday":
            return False
        return True

emp_1 = Employee("corey", "schafer", 5000)
emp_2 = Employee("Rai", "Rai", 6000)
if Employee.is_workday("Tuesday"):
    print("workday")
```
Static methods are simply functions that live inside the namespace of the class.They are just under the namespace of the class for convenience. They can be called from a class or from an instance.

### Inheritance and Subclasses
Inheritance allows a subclass to reuse and extend the attributes and methods of an existing class
```py
class Employee:
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
class Developer(Employee):
    pass
dev_1 = Developer("corey","schafer",5000)
dev_2 = Developer("Rai","Rai",6000)
print(help(Developer))
```
When we instantiated python looked for an `__init__` method in developer class but did not find it, And then looked for `__init__`
method in its parent class i.e., `Employee`
```py
Help on class Developer in module __main__:

class Developer(Employee)
 |  Developer(fname, lname, pay)
 |
 |  Method resolution order:
 |      Developer
 |      Employee
 |      builtins.object
 |
 |  Methods inherited from Employee:
 |
 |  __init__(self, fname, lname, pay)
 |      Initialize self.  See help(type(self)) for accurate signature.
 |
 |  ----------------------------------------------------------------------
 |  Data descriptors inherited from Employee:
 |
 |  __dict__
 |      dictionary for instance variables (if defined)
 |
 |  __weakref__
 |      list of weak references to the object (if defined)
```
The last print gives helpful information about the order of methods and other useful informations   
```py
class Employee:
    raise_ = 1.05
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
    def apply_raise(self):
        self.pay = int(self.pay*self.raise_)
class Developer(Employee):
    raise_ = 1.10
dev_1 = Developer("corey", "schafer", 5000)
dev_2 = Employee("Rai", "Rai", 6000)
print(dev_1.pay)
dev_1.apply_raise()
print(dev_1.pay)
print(dev_2.pay)
```
By changing the raise amount in our subclass it didnt have any effect on our employee instances,We can make changes to the subclass
without changing it in parent class

```py
class Employee:
    raise_ = 1.05
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.email = fname + lname + "@gmail.com"
    def apply_raise(self, raise_):
        self.raise_ = raise_
    def full_name(self):
        self.full_name_ = self.fname + self.lname
        return self.full_name_
class Developer(Employee):
    def __init__(self, fname, lname, pay, prog_lang):
        super().__init__(fname, lname, pay) #Employee.__init(self,fname,lname,pay), another way people use
        self.prog_lang = prog_lang
class Manager(Employee):
    def __init__(self, fname, lname, pay, employees=None):
        super().__init__(fname, lname, pay) #Employee.__init(self,fname,lname,pay), another way people use
        if employees is None:
            self.employees = []
        else:
            self.employees = employees
    def add_emp(self, emp):
        if emp not in self.employees:
            self.employees.append(emp)
    def rem_emp(self, emp):
        if emp in self.employees:
            self.employees.remove(emp)
    def print_emp(self):
        for emp in self.employees:
            print("-->", emp.full_name())
dev_1 = Developer("corey", "schafer", 5000, "python")
dev_2 = Developer("Rai", "Rai", 6000, "java")
mgr_1 = Manager("sue", "smith", 70000, [dev_1])
print(mgr_1.email)
mgr_1.add_emp(dev_2)
mgr_1.print_emp()
print(isinstance(mgr_1, Manager))
print(isinstance(mgr_1, Employee))
print(issubclass(Developer, Employee))
print(issubclass(Manager, Employee))
print(issubclass(Manager, Developer))

```

### Special methods/magic methods
Two special methods `__repr__` which is made for developers and `__str__` is for users.
The form of repr's return is same as how the instantiation's RHS is `Employee("Corey", "Schafer", 50000)`.
The str is just a print to show info about the object
```py
lists = []
class Employee:
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
        self.fullname = self.fname + self.lname
        self.email = fname + lname + "@gmail.com"
    def __repr__(self):
        return f"Employee('{self.fname}','{self.lname}','{self.pay}')"
    def __str__(self):
        return f"{self.fullname} - {self.email}"
emp_1 = Employee("Corey", "Schafer", 50000)
emp_2 = Employee("rai", "rei", 2500)
print(emp_1)
print(str(emp_1))
print(repr(emp_1))
lists.append(emp_1)
lists.append(emp_2)
print(lists)
```
this prints out to 
```
001 | CoreySchafer - CoreySchafer@gmail.com
002 | CoreySchafer - CoreySchafer@gmail.com
003 | Employee('Corey','Schafer','50000')
004 | [Employee('Corey','Schafer','50000'), Employee('rai','rei','2500')]
```
the containers display the object as its repr! but actually the object stored is at a memory with its all its attributes and methods etc....

another special method is `__add__` to add some attribute of the object or if the object is a number then the number itself gets added like how 2 integers get added.

```py
class Employee:
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.pay = pay
    def __add__(self, other):
        return (self.pay + other.pay)
    
emp_1 = Employee("Corey", "Schafer", 50000)
emp_2 = Employee("rai", "rei", 2500)
print(emp_1.__add__(emp_2))
```
An exmaple of add method 
There are a lot of magic methods like these which can be seen at python docs that are attached below:
1.[Emulating generic types](https://docs.python.org/3/reference/datamodel.html#emulating-generic-types)  
2.[Emulating callable objects](https://docs.python.org/3/reference/datamodel.html#emulating-callable-objects)  
3.[Emulating container types](https://docs.python.org/3/reference/datamodel.html#emulating-container-types)  
4.[Emulating numeric types](https://docs.python.org/3/reference/datamodel.html#emulating-numeric-types) - Like the `__add__` method  
5.[Emulating buffer types](https://docs.python.org/3/reference/datamodel.html#emulating-buffer-types) - IDK what this is XD  
but normally only some of them will be used 

### Property decorators - getters, setters and deleters

```py
class Employee:
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.email = fname + lname + "@gmail.com"

    def fullname(self):
        """returns a fullname string"""
        return ("{} {}".format(self.fname, self.lname))

emp_1 = Employee("corey", "schafer", 5000)

print(emp_1.fname)
print(emp_1.email)
print(emp_1.fullname())
```
This gives an output  
```
corey
coreyschafer@gmail.com
corey schafer
```
but
```py
class Employee:
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname
        self.email = fname + lname + "@gmail.com"

    def fullname(self):
        """returns a fullname string"""
        return ("{} {}".format(self.fname, self.lname))

emp_1 = Employee("corey", "schafer", 5000)
emp_1.fname = "jojo"

print(emp_1.fname)
print(emp_1.email)
print(emp_1.fullname())
```
gives an output 
```
jojo
coreyschafer@gmail.com
jojo schafer
```

so to fix this we do:

```py
class Employee:
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname

    def email():
        return ("{}.{}@gmail.com".format(self.fname, self.lname))

    def fullname(self):
        """returns a fullname string"""
        return ("{} {}".format(self.fname, self.lname))

emp_1 = Employee("corey", "schafer", 5000)
emp_1.fname = "jojo"

print(emp_1.fname)
print(emp_1.email())
print(emp_1.fullname())
```
but anyone who is using our class-their code breaks so to continue using the email as an attribute we do...

```py
class Employee:
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname

    @property
    def email():
        return ("{}.{}@gmail.com".format(self.fname, self.lname))

    def fullname(self):
        """returns a fullname string"""
        return ("{} {}".format(self.fname, self.lname))

emp_1 = Employee("corey", "schafer", 5000)
emp_1.fname = "jojo"

print(emp_1.fname)
print(emp_1.email)
print(emp_1.fullname())
```
so now we are able to access email like an attribute
thats how we use getters  
  
now if we use:
```py
class Employee:
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname

    @property
    def email():
        return ("{}.{}@gmail.com".format(self.fname, self.lname))

    @property
    def fullname(self):
        """returns a fullname string"""
        return ("{} {}".format(self.fname, self.lname))

emp_1 = Employee("corey", "schafer", 5000)
emp_1.fullname = "jojo boi"

print(emp_1.fullname)
```
this gives an error so now we use the setter

```py
class Employee:
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname

    @property
    def email():
        return ("{}.{}@gmail.com".format(self.fname, self.lname))

    @property
    def fullname(self):
        """returns a fullname string"""
        return ("{} {}".format(self.fname, self.lname))
    
    @fullname.setter
    def fullname(self, name):
        """returns a fullname string"""
        first , last = name.split(" ")
        self.first = first
        self.last = last


emp_1 = Employee("corey", "schafer", 5000)
emp_1.fullname = "jojo boi"


print(emp_1.fullname)
```
this gives output:
```
corey schafer
```
now deleter
```py
class Employee:
    def __init__(self, fname, lname, pay):
        self.fname = fname
        self.lname = lname

    @property
    def email():
        return ("{}.{}@gmail.com".format(self.fname, self.lname))

    @property
    def fullname(self):
        """returns a fullname string"""
        return ("{} {}".format(self.fname, self.lname))
    
    @fullname.setter
    def fullname(self, name):
        """returns a fullname string"""
        first , last = name.split(" ")
        self.first = first
        self.last = last

    @fullname.deleter
    def fullname(self):
        print("delete name")
        self.fname = None
        self.lname = None


emp_1 = Employee("corey", "schafer", 5000)
emp_1.fullname = "jojo boi"
del emp_1.fullname 
print(emp_1.fullname)
```