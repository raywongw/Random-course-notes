
[[COMP2396 Chapter 7 - Abstract Classes and Interfaces|Last Chapter]] [[COMP2396 Chapter 9 - GUI and Event Handling|Next Chapter]]


### Object
* Every class in Java ``extends`` the **Object** class
* **Object** class is the **superclass** of everything
* avaliable methods:
	* `equals(Object obj)`
		* true if both reference variables refer to the same object
		* override both this method to check the contents of two object
	* `getClass()`
		* return a Class Object tha
	* `hashCode()`
		* if two objects are equal then they have the same result of ``hashCode()``
	* `toString()`
		* class name + '@' + hash code in hex form

##### Use Object as Polymorphic Type
- type-safety
- Have costs when using Object a

###### Examples of code that cannot be compiled
```Java
ArrayList <Object> myDogArrayList = new ArrayList <Object>();
Dog aDog = new Dog();
myDogArrayList.add(aDog);
Dog d = myDogArrayList.get(0);
```
- The object ArrayList accepts anything(String, Integer, Dog, etc.)
- the get method expects to return a Object but not a specific class


```Java
public class BadDog2 {
	public static void main(String[] args) {
		Dog dog = new Dog();
		Object sameDog = getObject(dog);
		sameDog.makeNoise();
	}
	public static Object getObject(Object o){
		return o;
	}
}
```
- Code would not compile since the Object instance `sameDog` does not have `makeNoise()` method



##### Objects are object
Take object is a core of a object, where any subclass is a outer layer of the superclass
Outer layer can access inner layer, but cannot access outer layer
- Object has access to methods to itself only



### Cast
* **cast** can also be applied to object reference:
```Java
Dog dog = new Dog();
Object o = dog;	//ISA
Dog sameDog = (Dog) o; //cast
```


* ``instanceof`` operator: check if an object is an instance of a certain class
```Java
Object o = new Dog();
if (o instanceof Dog) {
	System.out.println("It is a Dog");
}
```