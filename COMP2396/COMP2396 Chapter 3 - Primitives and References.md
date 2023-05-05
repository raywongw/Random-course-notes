
[[COMP2396 Chapter 2 - Classes and Objects|Last Chapter]] [[COMP2396 Chapter 4 - State and Behavior of an Object|Next Chapter]]

## Primitives and References

#### Varibale Declaration
* Declare before use
* type and name

#### Primitive Types
* 8 primitive types: boolean, char, byte, short, int, long, float, double 
```Java
double PI = 3.14159;
float PI_F = 3.14159f; //Java treats number with floating point as double 'f' specify them as a float
```
* Type conversion: 
	* compiler doesn't allow cast wider range to narrower range (as this might result in information loss)
	* we must explicitly tell the compiler we want to cast
	
#### References
* **object reference variables** instead of **object variables**
* holds **way to access** a specific object
* doesn't hold **actual value**
```Java
Book b = new Book();
Book c = new Book();
Book d = c; //d refers to the same object as c, so we haven't create any new object
```

#### Array
* holds primitive types or reference variable
```Java
int[] nums = {6, 19, 44, 42};\\or
int[] arrs = new int[4];
```