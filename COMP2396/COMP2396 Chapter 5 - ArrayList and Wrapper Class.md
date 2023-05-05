
[[COMP2396 Chapter 4 - State and Behavior of an Object|Last Chapter]] [[COMP2396 Chapter 6 - Inheritance and Polymorphism|Next Chapter]]
## Arrays
- Similar to C++ Array


## ArrayList
 - fill what [[#Arrays]] cannot do
	 - Grow or shrink array size to add or delete item to array
	 - Know a certain thing is in the list without traversing the list
	 - retrieve items in array without exact slot
- type of ArrayList must be a class, not primitive type 
	- use [[#Wrapper Class|wrapper class]] to do so, `ArrayList<Integer> nums = new ArrayList<Integer>();`

```Java
import java.util.ArrayList;

// create an ArrayList
ArrayList<Egg> myList = new ArrayList<Egg>();
// put something into it
Egg a = new Egg();
myList.add(a);
// put another thing into it
Egg b = new Egg();
myList.add(b);
int theSize = myList.size();
// find out if it contains something
boolean isIn = myList.contains(a);
for (Egg egg : myList) {
// egg.xxxx
}
```

##### Avaliable methods:
* ``add(Object elem)``
* ``remove(int index)``
* ``remove(Object elem)``
* ``contains(Object elem)``
* ``isEmpty()``
* ``indexOf(Object elem)``
* ``size()``
* ``get(int index)``


##### Specify integer in remove methods
###### ``remove(int index)``
- removes an item at desired index

###### ``remove(Object elem)``
- removes the element in the array
	- For `int`, use `ArrayList.remove((integer) n)` to distinguish from [[#``remove(int index)``|remove (index)]]




## Packages

##### Advantages
- organization
- name-scoping
	- prevent name collision
- security
- no impact of efficiency for `java.lang.*`
##### Class' full name
- package name + class name
- **Must be specified** when class in a package other than ``java.lang`` is used
- imprt all classes in a package (E.g. ``java,util``) to avoding typing the full name:
```Java
import java.util.*;
```




## Wrapper Class

* classes correspond to primitive types: as ``ArrayList`` only supports class

primitive  type | wrapper class | unwrap function
----------------|---------------|----------------
boolean | Boolean | booleanValue()
char | **Character** | charValue()
byte | Byte | 
short | Short |  
int | **Integer** | intValue()
long | Long | 
float | Float | 
double | Double | doubleValue()

* wrap and un wrap:
```Java
boolean b = true;
Boolean bWrap = new Boolean(b);
boolean bUnWrap = bWrap.booleanValue();
```

##### Autoboxing
- automatically conversion between primitive types and wrapper classes
-  works in assigning value, method arguments, return values, arithmetics, boolean expression
```Java
int i = new Integer(981);
```

-  static method to parse a string to a primitive:
```Java
double d = Double.parseDouble("420.24");
boolean b = Boolean.parseBoolean("True");
```

* static method to parse a primitive to a string:
```Java
double d = 42.5;
String doubleString = "" + d; // concatenating
String anotherDoubleString = Double.toString(d);//static method
```

#### Number Formatting
```Java
float a = 4.333;
String s = String.format("This cat weights %.2fkg", a );
```
foramt | meaning
-------|--------
%,d| insert **commas**, format as integer
%.2f| float with precision of **2** decimal places
%,.2f|  
%,5.2f | 5 means at least 5 characters wide, padding spaces and zeros
%h | hexadecimal
%c | character


