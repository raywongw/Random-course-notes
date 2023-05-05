
[[COMP2396 Chapter 3 - Primitives and References|Last Chapter]] [[COMP2396 Chapter 5 - ArrayList and Wrapper Class|Next Chapter]]

## State and Behaviour of an object
* Instances of the same class have **same instance variables** and **same methods** but actual value may be different

#### Parameters
* **pass-by-value**

#### Methods
* Getters and setters (**Encapsulation**)
	* Getter: get values of variable in a class
	* Setter: assign value to a variable in class
* Constructor
	* called automatically when an object is created
	* **same name** as the class
	* **no** return type
	* can be overloaded
	* **default constructor** will only be defined for a class when there is no other constructor
		* Always provide a no-argument constructor whenever possible
	* **Inheritance**
		* constructors are **not inherited**
		* **constructor chaining** to the **no no-argument constructor** of its superclass
			* e.g. caller -> class no-argument constructor -> superclass no-argument constructor
		- Another way to call superclass constructor
		```Java
public Class pig{
	public Pig(int n){
		super(n)
	}
}
```


#### Static 
* **Static Method**: methods doesn't depend on the value of instance variable
	* can run withtour any instance of the class
```Java
	Math.round( 3.14 ); //Math is class name and round() is a static method
``` 
	* can't use any **non-static** instance variables
	* can't use other **non-static** methods
* **Static Variable**: 
	* **shared** by all instances of a class
	* **initialized** when the class loaded for the first time
	* can be accessed using **class name**
	* can be used in **static methods** 


#### Final
* **no default value**
* can not be changed
```Java
public final int volume = 330;
```
* to define a constant
```Java
public static final double PI = 3.141592653589793;
```
* **static initializer**: run after the class is loaded and any static method can be used
```Java
public class Foo2 {
	public static final int FOO_X;
	static {
		FOO_X = 25;
	}
}
```
* **final method** cannot be overridden
* **final class** cannot be extended
	
#### Variable Initialization
* Instance variable get default value if not assigned:  

 type | default value
 ------|--------------
 number primitive | 0
 boolean | false
 object references | null
 
* Local variable: **must be initialized** before used

#### Comparison 
* `==`: check whether L.H.S and R.H.S's bit patterns are the same and extra bits will be ignored


































