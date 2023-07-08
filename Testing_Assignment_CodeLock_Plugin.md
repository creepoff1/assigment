# Within the scope of the given task, the CodeLock plugin for IntelliJ IDEA 7 was tested, and the following bugs were found:

## 1. Class or region locking. The code is highlighted with a blue background only after placing the cursor in the editor
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class2 {
}
```
### STR:
-	Open the Project tree
-	Open Class1 in the editing window
-	Select "Class1" in the tree
-	Invoke the context menu by right-clicking
-	Select "CodeLock" from the context menu
-	Press "Code Lock"
### Result:
The code in the editing window is not highlighted with a blue background, only after placing the cursor in the editing window, the code is highlighted with a blue background
### Expected result:
The code in the editing window is instantly highlighted with a blue background

## 2. Unlocking the class or region. The code stops being highlighted with a blue background only after placing the cursor in the editor
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
}
```
-	Class1 is locked and highlighted with a blue background
### STR:
-	Open the Project tree
-	Open Class1 in the editing window
-	Open the CodeLock menu
-	The locked class is displayed in the list of elements
-	Select Class1
-	Press "Remove <<" button
### Result:
The code in the editing window is not cleared from the blue background until the cursor is placed in the editing window
### Expected result:
The code is cleared from the blue background immediately after unlocking

## 3. Is it possible to refactor locked code
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
}
```
-	Class1 is locked and highlighted with a blue background
### STR:
-	Open the Project tree
-	Open Class1 in the editing window
-	Right-click on the class name
-	Select "Refactor" from the context menu
-	Select "Rename" from the context menu
-	Enter a new name for the class: Class1_new
-	Press "Refactor"
### Result:
The class name has been changed
### Expected result:
The class name should not be changed, as the class is locked

## 4. It is possible to remove the locked class from the project tree
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
}
```
-	Class1 is locked and highlighted with a blue background
### STR:
-	Open the Project tree
-	Select Class1
-	Right-click on the Class1
-	Select "Delete" from context menu
-	Press  "OK"
### Result:
Class1 has been deleted
Codelock displays Class1 as locked
### Expected result:
Class1 cannot be deleted because it is locked

## 5. It is possible to lock an already locked region
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
	private int myNumber;
	private String myText;
}
```
-	The region ```private String myText;``` is locked
### STR:
-	Open the Project tree
-	Open Class1 in the editing window
-	Highlight the line ```private String myText;```
-	Right-click on the line ```private String myText;```
-	Select "CodeLock" from context menu
-	Select "Lock region" from context menu
### Result:
Check Codelock tool window ->  Regions

A region with the same "from" and "length" values has been added again
### Expected result:
It should be impossible to add duplicate regions

## 6. GoTo for regions, the cursor should be placed at the beginning or end of the locked region
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
	private int myNumber;
	private String myText;
}
```
-	The region ```private String myText;``` is locked
### STR:
-	Open the CodeLock menu
-	Select "Regions"
-	Select the locked region
-	Press the "GoTo.." button
### Result:
Class1 opened in the editing window, but the cursor was not placed at the beginning or end of the locked region
### Expected result:
The cursor is placed at the beginning or end of the locked region

## 7. Is it possible to lock an empty region
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
	private int myNumber;
	private String myText;
}
```
### STR:
-	Open the Project tree
-	Open Class1 in the editing window
-	Place the cursor anywhere in the code
-	Right-click
-	Select "CodeLock" from context menu
-	Select "Lock region" from context menu
### Result:
Check CodeLock tool window -> Regions
A new region has been added, but it is not highlighted with a blue background, making it difficult to understand what exactly has been locked
### Expected result:
It is not possible to lock an empty region

## 8. Remove multiple regions may require multiple attempts to delete the last one
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
	private int myNumber;
	private String myText;
}
```
-	The region ```private String myText;``` is locked
-	The Region ```private int myNumber;``` is locked
### STR:
-	Open the CodeLock menu
-	Select "Regions"
-	Select the first locked region
-	Press the "Remove <<" button
-	Select the second locked region
-	Press the "Remove <<" button
### Result:
The second region is not being deleted, and it requires multiple attempts to remove it
### Expected result:
The second region is deleted on the first attempt

## 9. Unnecessary warning when deleting regions
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
	private int myNumber;
	private String myText;
}
```
-	The region ```private String myText;``` is locked
### STR:
-	Open the CodeLock menu
-	Select "Regions"
-	Select the locked region
-	Press the "Remove <<" button
### Result:
Unnecessary warning with the text "The Element you are removing has children. Are you sure you want to remove it?"
### Expected result:
There are no warnings during the deletion of a region. A region is a part of the code and does not have any children.

## 10. It is possible to lock an interface
### Preconditions:
-	The project contains an interface named "Interface1" with the following code:
```
package mypackage;

public interface Interface1 {
}
```
### STR:
-	Open the Project tree
-	Select Interface1
-	Right-click on the Interface1
-	Select "CodeLock" from context menu
-	Select "Lock code" from context menu
### Result:
Interface1 has been locked and is displayed in the list of locked elements as a class
### Expected result:
Interface1 cannot be locked (there is no mention of such functionality in the plugin description).

## 11. The class is locked, and there is incorrect tree expansion display in the CodeLock menu
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
}
```
-	Class1 is locked and highlighted with a blue background
### STR:
-	Open the CodeLock menu
-	Select "Elements"
-	Open the folder "Class1.java" of the class in the tree
### Result:
The plus icon to expand the tree is displayed next to the "Class1"
### Expected result:
There are no plus icons to expand the tree for the locked class as the class is fully locked

## 12. It is not possible to lock a nested class as an element
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
	public class NestedClass1 {
		}
}
```
### STR:
-	Open the Project tree
-	Open Class1 in the editing window
-	Place the cursor on "NestedClass1"
-	Right-click
-	Select "CodeLock" from context menu
-	Select "Lock code" from context menu
### Result:
The "NestedClass1" was not locked
### Expected result:
The "NestedClass1" class has been locked

## 13. CodeLock Graph does not show nested classes and methods of a locked class
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
	public class NestedClass1 {
		private int myNumber;

		public int getNumber() {
			return myNumber;
			}
		}
}
```
-	Class1 is locked and highlighted with a blue background
### STR:
-	Open the Project tree
-	Open Class1 in the editing window
-	Right-click
-	Select "CodeLock" from context menu
-	Select "CodeLock Graph" from context menu
### Result:
CodeGraph does not display nested classes, methods, and fields
### Expected result:
CodeGraph shows nested classes, methods, and fields
```
P.S.
The CodeLock CodeGraph functionality is highly debated. Firstly, it duplicates the functionality of CodeGraph. Secondly, it requires the code to be locked before building the diagram through CodeLock CodeGraph.
It is necessary to clarify the requirements for the CodeLock CodeGraph functionality
```
## 14. Unexpected behavior. Locking a class that already contains a locked method
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
	private int myNumber;

	public int getNumber() {
		return myNumber;
	}
}
```
-	Method ```getNumber``` is locked and highlighted with a blue background
### STR:
-	Open the Project tree
-	Open Class1 in the editing window
-	Right-click on Class1
-	Select "CodeLock" from context menu
-	Select "Lock Code" from context menu
### Result:
It is not possible to lock Class1 + some side effects like:
It is not possible to unlock the method "getNumber". It is removed from the list of elements but remains locked for editing
### Expected result:
It is possible to lock Class1

## Gray out actions
