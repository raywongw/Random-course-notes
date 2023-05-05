
[[COMP2396 Chapter 6 - Inheritance and Polymorphism|Last Chapter]] [[COMP2396 Chapter 8 - The Ultimate Superclass - Object|Next Chapter]]
### Abstract Class
- cannot be made into a instance variable
- May have both concrete method and abstract method

### Concrete Class
- Must implement all abstract methods from its superclasses
	- Similar to [[COMP2396 Chapter 6 - Inheritance and Polymorphism#Method Overriding|Overriding]]


### Abstract Method
- without method body
```Java
public abstract void something();
```



### Concrete method
- Must have a method body
```Java
public void something(){
	/* do something*/
}
```



### Deadly Diamond of Death
- D inherits from B, C and B, C inherits from A
- Compiler don't know which method or variable should available for class D


### Interface
- Solve [[#Deadly Diamond of Death|multiple inheritance problem]]
- Pure[[#Abstract Class| abstract class]]
- All abstract method
- Can be used as polymorphic type
- Use when it should be allowed to be used by any classes, neglecting the inheritance tree

Example of interface:
```Java
public interface animal{
	/* public abstract is optional here*/
	void eat();
	public abstract void play();
}
```


```Java
public class ragdoll extends Cat implements animal{
	/* implement methods from animal interface*/
	void eat(){/* something */ }
	void play(){/* domething */}
}
```


































## Abstract Classes and Interfaces

#### abstract class
class that can not be instantiated

* a class must be **abstract** if it has at least one **abstract method**

```Java
abstract class Canine extends Animal {
	public void roam() { ... }
}
```
#### abstract method
method has **no method body** and hence must be **extended** 
```Java
public abstract void eat();
```
* a **concrete class** must implements all the **abstract method** it inherits
* an **abstract class** may not need to do so

#### interface
* **interface** is a **pure abstract class** with all method being **abstract** 
* solve the problem of restriction of **multiple inheirtance**
```Java
public interface Pet {
	public abstract void beFriendly();
	public abstract void play();
}
```
* Interface methods are implicitly
**public** and **abstract**
* ``implement`` a **class** ``implements`` the ``interface`` must implement all the interface's methods
* a class may ``implements`` multiple interfaces

#### general design rule
* class
* subclass
* abstract class
* interface