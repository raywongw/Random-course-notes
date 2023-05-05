
[[COMP2396 Chapter 1 - Introduction|Last Chapter]] [[COMP2396 Chapter 3 - Primitives and References|Next Chapter]]
#### Advantages of OOP
* **Modularity**
* **Information hiding**
* **Code re-use**
* **Pluggability**


#### Class
* Blueprint of an object 
	* class tells virtual machine how to make an object of that type
* abstract both **state** and **behavior** of the objects created from the class


#### Object
* An instance of class
* Instance vairable: 
	* things an object **know** about itself
	* **state/data** of an object
	* differ from object to object
* Method:
	* thins an object **does**
	* **behavior** of an object
	* **operate on data** of an object
* Define a Class:
```Java
class Dog{
	//instance variable 
	
	//methods' definition
}
```
* Inherit from superclass:
```Java
class Poodle extends Dog
```
* **main()** Method:
	* **create** an object
	* **Call a method** of the object
	* name of the program is not included in the ``args``
```Java
public static void main(String[] args)
```

#### Garbage Collection
* objects live on **heap** 
* an object become eligible for **garbage collection** when it will never be used
* when system memory is low, **Garbage Collector** will run