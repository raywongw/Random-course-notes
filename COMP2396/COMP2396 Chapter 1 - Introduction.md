
[[COMP2396 Chapter 2 - Classes and Objects|Next Chapter]]

#### OOP v.s. PP
Procdedural Programming | Objec-Oriented Programming
------------------------|--------------------------- 
task | data
top-down design | bottom-up design
functions | classes

#### Trade Off:
* Security(Access Control)
* maintain&extend
* Code reusability

#### Objects in OOP
* Instances of the same class
	* have same  instance variables that represent their states to represent their **state**
	* actual values stored may be different
	* have same set of methods to represent their **behaviour**
	* actual behaviors **depend** their own states
* 




## Four principles of Objected-Orinted Programming

### Abstraction
representing essential features withour including backgroud details.
	* **WHAT** an object is
	* necessary and common properties
	* essential in **design**


### Encapsulation
wrapping data and operations into a single unit
	* information and implementation hiding
	* objects interact through public methods
	* essential in **implementation**


### Inheritance
- extend properties of one class to another class
- **subclass** inherits from **superclass**

- New method can be added to subclass
- aka Specialization
```Java
public class Animal{
	int hunger;
	String name;
	
	int food();
	void eat();
}

publoc class Cat{
	boolean breed;
	
	void play();
}
```

- IS-A relaton
	- Cat is an animal
	- An inheritance tree can be produced
	- e.g. Cat is a subclass of Animal, Ragdoll is a subclass of cat


### Polymorphism
- A class can take more than 1 form
- anything related to a superclass of object can be used on its subclass

- e.g. `Animal a = new Animal[5]`
	- The array can then hold cat or ragdoll since it is a subclass of Animal
- e.g. `void testClass(Animal)` takes Animal object
	- Cat or ragdoll class can also be used for the function







* **Inheritance**: objects of one class acquire the properties of objects of another class
	* a **subclass** can be derived from its **superclass**
	* **ISA TEST**: a subclass **is a** specialization of its superclass (inherit all its properties)(E.g. Cat is Animal)
* **Polymorphism**: able to take more than one form
	* making a call to the same method may results in different behaviors depending on the actual subclass object being called



#### Java
* Object-oriented
	* Everything is a class
* Platform independent
	* One java program can be compiled once to work on all platform
	* by Java Virtual Machines(JVM)
* Architectural-neutral 
	* Runing under Java Virtual Machine
* Java application
	* at least one class
	* **at least one** main() method
* **strong type**
* variable: primitive type and reference
* Loops: iterator is avaliable in Java
```Java
String[] names = { "Amanda", "Jessica", "Jacky" };
for ( String name : names ){
	System.out.println( name );
}
```
