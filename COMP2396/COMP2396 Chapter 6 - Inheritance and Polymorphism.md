
[[COMP2396 Chapter 5 - ArrayList and Wrapper Class|Last Chapter]] [[COMP2396 Chapter 7 - Abstract Classes and Interfaces|Next Chapter]]

### Instance Overview
- Put common code in a superclass
- Only methods can be overriden by its subclass
	- Variable would not be overriden as it inherits from superclass
- New instance variable can be added to the subclasses (Specialization)

```Java
public class Doctor {
	boolean workAtHospital;
	void treatPatient() { /* perform a checkup */}
}

public class FamilyDoctor extends Doctor {
	boolean makesHouseCalls;
	void giveAdvice(){/* give homespun advice */}
}

public class Surgeon extends Doctor {
	void treatPatient(){/* perform surgery */} 
	void makeIncision(){/* make incision */}
}
```


### Inheritance Tree Design
1. Design a superclass that hold common attribute and behavior
	- Avoid code suplication among subclass
2. See if subclasses requires specific methods/override methods
3. 


### Access Control
- Public members of a class can be inherited
- Private members cannot be inherited, but can be access with public getter/setter


- Four level of access
| Access Level | Access Modifier | Class | Package | Subclass | World |
| ------------ | --------------- | ----- | ------- | -------- | ----- |
| Private      | `private`         | Y     | N       | N        | N     |
| default      | (none)          | Y     | Y       | N        | N     |
| protected    | `protected`       | Y     | Y       | Y        | N     |
| public       | `public`          | Y     | Y       | Y        | Y      |


### IS-A v.s. HAS-A
- IS-A uses inheritance
- HAS-A puts object in its instance object


### Rules in inheritance design
- use injeritance when
	- Subclass is a specialization of superclass
	- Subclass shares common behavior with superclass
- Do not use inheritance when
	- subclass does not pass IS-A test with superclass


### Method Overriding
```Java
public class Animal{
	void makeNoise(){/*noise*/}
}

public class Cat extends Animal{
	@override
	void makeNoise(){/*some other noise*/}
}
```
- Argument list must be same
- Return type must be a same/compatible subclass type
- Cannot be less accessible (e.g. public -> private)


### Method Overloading
```Java
public class Animal{
	makeNoise(){/*noise*/}
}

public class Cat extends Animal{
	//overload method
	makeNoise(int i){/*some other noise*/}
}
```
- Argument list must be different
- Return type can be different subclass type
- Can have different access level (e.g. public -> private)



### Polymorphism
```Java
Animal dog1 = new Dog()
```
- Reference type can be superclass of actual object
	- as long as they pass IS-A Test
- Methods added in `Dog` Class would not be available to `dog1`
