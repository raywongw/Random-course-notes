

[[COMP2396 Chapter 9 - GUI and Event Handling|Last Chapter]] [[COMP2396 Chapter 11 - Network and Multi-threading|Next Chapter]]
# Serialization and File I/O
- save and load state of different class

##### Steps in serializing an object
- Make `FileOutputStream`
	- a `.sav` is created automatically if it does not exist
- Make `ObjectOutputStream` 
- Write objects by `ObjectOutputStream`
- Close the `ObjectOutputStream`

Example
```Java
// Step 1
FileOutputStream fileStream = new FileOutputStream(FileOutputStream("MyGame.sav");`
// Step 2
ObjectOutputStream os = new ObjectOutputStream(fileStream);
// Step 3 (order same as restoring)
os.writeObject(/*any object*/)
// Step 4
os.close();
```

- a `.sav` is created, which stands for serialization file

##### Steps in restoring objects
- Make a `FileInputStream`
- Make an ObjectInputStream
- Read and cast objects in same order as loading objects
- Close ObjectInputStream
	- FileInputStream is closed automatically

Example
```java
// Step 1
FileInputStream fileStream = new FileInputStream("MyGame.sav");
// Step 2
ObjectInputStream os = new ObjectInputStream(fileStream);
// Step 3 (orer same as serializing)
GameCharacter elf = (GameCharacter) os.readObject();
GameCharacter troll = (GameCharacter) os.readObject();
GameCharacter magician = (GameCharacter) os.readObject();
// className variableName = (className) os.readObject();

// Step 4
os.close();
```



### Connection streams
Example: `FileOutputStream` connects to file and send data to the file
- a connection to a source/destination (file/socket)

### Chain stream
Example: `ObjectOutputStream` convert objects to data and sent to a connection stream (`FileOutputStream`)
- only works when chained to another stream
- provide high level method for serialiation


### Serializing an Object
- Whole object graph is saved
	- All member and its superclass is saved
	- If 2 same obj is saved, it will only save 1 object and add pointer for another
- fails if an object in graph is not serializable

- Mark Runtime-specific variable as `transient`
	- `transient connectionSocket;`
	- default values are given to transient variable

### Serializable Interface
- a marker to tell compiler that a class can be serialized
- It's subclass are automatically serializable


### Serial versioning
- Generated after serialization of object
- Class have different `serialVersionUID` if class is modified
	- cannot be serialized if `serialVersionUID` of serialized object and the corresponding class
	- bypassing it by assigning a `serialVersionUID`
		- `private static final long serialVersionUID = 6385147890911367760L;`
		- make sure it is compatible with previous class


##### Changes to a class that hurt deserialization
- Deleting an instance variable
- Changing the declared type of an instance variable
- Changing a non transient instance variable to transient
- Moving a class up or down the inheritance hierarchy
- Changing a class (anywhere in the object graph) from serializable to non serializable
- Changing an instance variable to static


##### Changes to a class that **usually** OK to serialization
- Adding new instance variable to the class (existing objects will deserialize with default values for the instance variables they didn’t have when they were serialized)
- Adding classes to the inheritance tree
- Removing classes from the inheritance tree
- Changing the access level of an instance variable
- Changing an instance variable from transient to non transient (previously serialized objects will have a default value for the previously transient variables)




### Writing to Text file (.txt)
- `FileWriter` is used instead of `FileOutputStream`
- use try-catch
- txt file would not save before `FileWriter.close();` is called