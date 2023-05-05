
[[COMP2396 Chapter 12 - Life and Death of an Object|Last Chapter]] [[COMP2396 Summary|Summary]]

### Exceptions Class hierachy
- Superclass - Throwable
- Subclass under throwable - Exception and Error
	- Error cannot be fixed
	- Exception can be handled




### Handle Exception
- Use Try-catch-finally block
	- Try block holds risky operations that can cause error
	- Exception holds the operation when handling error
		- Can have multiple catch block for different exceptions
	- Finally holds whatever should be run before returning in try block or catch block
- 2 possible case
	- Try block runs smoothly, good ending
	- Try block has error, exception is thrown, bad ending
```Java
public void crossFinger() {
	try{
		anObject.riskyOperation();
	} catch (Exception ex){
		System.out.println("Aaauuggh!");
		ex.printStackTrace();
	}
	finally{
		System.out.println("No aaauuggh :)")
	}
}
```


### Unchecked exception
- Subclasses of Runtime exception
	- Ignored by compiler
- Usually problems in code logic
e.g. `NullPointerException, ArrayIndexOutOfBoundsException, ArithmeticException, IllegalArgumentException, NumberFormatException`

### Checked exception
- Exception that are not subclass of `RuntimeException`
- Must be thrown if there is a risky operation that throws checked exception



### Ducking exception




### Exception Rules
- cannot have catch block without try block
- cannot code between try and catch block
- try must be followed with catch OR finally
- must declare a 