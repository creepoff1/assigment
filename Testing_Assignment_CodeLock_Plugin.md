# Within the scope of the given task, the CodeLock plugin for IntelliJ IDEA 7 was tested, and the following bugs were found:

## 1. Class/Region locked. The code is highlighted with a blue background only after placing the cursor on the line
### Preconditions:
Project contains Class "Class1" with following code:
```
package mypackage;

public class Class2 {
}
```
### STR:
IDE -> Project tree -> Select Class1 in tree -> Right click -> Code Lock -> Lock Code
### Result:
The code is highlighted with a blue background only after placing the cursor on the line
### Expected result:
The code is highlighted with a blue background immediately after locking

## 2. Class/Region unlocked. The code is not cleared from the blue background highlighting until the cursor is placed on the line.
### Preconditions:
Project contains Class "Class1" with following code:
```
package mypackage;

public class Class1 {
}
```
Class1 is locked
### STR:
IDE -> Code lock side menu -> Select locked Class1 -> Press remove button
### Result:
The code is not cleared from the blue background highlighting until the cursor is placed on the line.
### Expected result:
The code is cleared from the blue background highlighting immediately after unlocking.

## 3. It is possible to refactor blocked code
### Preconditions:
Project contains class "Class1" with following code:
```
package mypackage;

public class Class1 {
}
```
Class1 is locked
### STR:
IDE -> Project tree -> Select Class1 in tree -> Open Class1 to edit -> Right click on class name -> Refactor -> Rename -> Type new name and press Refactor
### Result:
Class name is changed
### Expected result:
Impossible to change class name (code is locked)

## 4. It is possible to delete blocked code from Project tree
### Preconditions:
Project contains class "Class1" with following code:
```
package mypackage;

public class Class1 {
}
```
Class1 is locked
### STR:
IDE -> Project tree -> Select Class1 in tree -> Right click on Class1 -> Delete
### Result:
Class1 is deleted
CodeLock still shows Class1 as locked
### Expected result:
Class1 isn't deleted (code is locked)

## 5. It is possible to lock already locked region
### Preconditions:
Project contains class "Class1" with following code:
```
package mypackage;

public class Class1 {
	private int myNumber;
	private String myText;
}
```
Region 	```private String myText;``` is locked
### STR:
IDE -> Project tree menu -> Select Class1 in tree -> Open Class1 to edit -> mark string "private String myText;" -> Right click -> 	CodeLock -> Lock Region
### Result:
Check Codelock tool window ->  Regions
2 same regions are shows
### Expected result:
It's impossible to add the same region twice

## 6. Goto for Regions. The cursor is not set at the beginning or end of the locked region
### Preconditions:
Project contains class "Class1" with following code:
```
package mypackage;

public class Class1 {
	private int myNumber;
	private String myText;
}
```
Region 	```private String myText;``` is locked
### STR:
IDE -> Codelock tool window -> Regions -> Select blocked region -> GoTo..
### Result:
File Class1 opened but the cursor is not set at the beginning or end of the locked region
2 same regions shows
### Expected result:
The cursor is set at the beginning or end of the locked region

## 7. Is it possible to lock an empty region
### Preconditions:
Project contains class "Class1" with following code:
```
package mypackage;

public class Class1 {
	private int myNumber;
	private String myText;
}
```
### STR:
IDE -> Project tree menu -> Open Class1 -> Put cursor on an empty string -> Right click -> CodeLock -> Lock Region
### Result:
Check CodeLock tool window -> Regions
New region added
### Expected result:
Impossible to lock an empty region

## 8. Remove few blocked regions. It's needed a few attempts to remove last region
### Preconditions:
Project contains class "Class1" with following code:
```
package mypackage;

public class Class1 {
	private int myNumber;
	private String myText;
}
```
Region 	```private String myText;``` is locked
Region ```private int myNumber;``` is locked
### STR:
IDE -> CodeLock tool window -> Regions -> Delete 1-st region -> Delete 2-nd region
### Result:
2-nd region don't deleted (still in list), it's needed a few attemtps to remove last region
### Expected result:
2-nd region deleted by one attmept

## 9. Unnessesary warning message for removing region
### Preconditions:
Project contains class "Class1" with following code:
```
package mypackage;

public class Class1 {
	private int myNumber;
	private String myText;
}
```
Region 	```private String myText;``` is locked
### STR:
IDE -> CodeLock tool window -> Regions -> Press Remove region
### Result:
Unnessesary warning message with text "The Element you are removing has children Are you sure you want to remove it?"
### Expected result:
There is no warning messages, Region it's a part of code and has not "chidlren"


## 10. It is possible to lock an interface
### Preconditions:
Project contains interface "Interface1" with following code:
```
package mypackage;

public interface Interface1 {
IDE -> CodeLock tool window ->
}
```
### STR:
IDE -> Project tree menu -> select Interface1 -> Right click on interface name -> CodeLock -> Lock Code
Check IDE -> CodeLock tool window -> Elements
### Result:
The Interface1 is locked and displayed in the list of locked items as a class.
### Expected result:
The Interface1 cannot be locked and is not displayed in the list of items

## 11. Lock Class. Wrong expansion of the tree.
### Preconditions:
Project contains interface "Class1" with following code:
```
package mypackage;

public class Class1 {
}
```
Class1 is locked
### STR:
IDE -> CodeLock tool window -> Elements
Open folder Class1.java
### Result:
There is a plus sign to expand the tree for Class1
### Expected result:
There is no a plus sign to expand the tree for Class1, because Class1 is entirely locked

## 12. It is impossible to lock nested class as element.
### Preconditions:
Project contains interface "Class1" and nested "NestedClass1" with following code:
```
package mypackage;

public class Class1 {
	public class NestedClass1 {
		}
}
```
### STR:
IDE -> Project tree menu -> Open Class1 -> Put cursor on "NestedClass1" -> Right click -> CodeLock -> Lock Code
### Result:
NestedClass1 was not locked.
### Expected result:
NestedClass1 was locked.

## 13. It is impossible to lock method in nested class as element
### Preconditions:
Project contains interface "Class1" and nested "NestedClass1" with following code:
package mypackage;
```
public class Class1 {
	public class NestedClass1 {
		private int myNumber;
		
		public int getNumber() {
			return myNumber;
			}
		}
}
```
### STR:
IDE -> Project tree menu -> Open Class1 -> Put cursor on "getNumber" method -> Right click -> CodeLock -> Lock Code
### Result:
getNumber method was not locked.
### Expected result:
getNumber method was locked.

## 14. CodeLock conxtext menu "CodeLock Graph" is not worked
### Preconditions:
Project contains interface "Class1" with following code:
```
package mypackage;

public class Class1 {

}
```
### STR:
IDE -> Project tree menu -> Open Class1 -> Put cursor on "Class1" -> Right click -> CodeLock -> CodeLock Graph
### Result:
IDE Fatal Error 
Error during dispatching of ...(logs in attachment)
### Expected result:
There are no any errors, Class1 is added to Code Graph menu as locked ??

## 15. 
