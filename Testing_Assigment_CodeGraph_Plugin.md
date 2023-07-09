# Within the scope of the given task, the CodeGraph plugin for IntelliJ IDEA 7 was tested, and the following bugs were found:
## 1. There is no tooltip displayed on the class
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
}
```
### STR:
-	Open the Project tree
-	Open Class1 in the editing window
-	Select "Class1" in the tree
-	Invoke the context menu by right-clicking
-	Select "CodeGraph" from the context menu
-	Press "Add Element"
-	Open Code Graph tool window
-	Place the cursor on Class1
### Result:
There is no tooltip displayed on the class
### Expected result:
There is tooltip displayed on the class

## 2. Add the package as an element through the project tree. IDE internal erorr occured
#### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
}
```
### STR:
-	Open the Project tree
-	Place the cursor on package "mypackage"
-	Invoke the context menu by right-clicking
-	Select "CodeGraph" from the context menu
-	Press "Add Element"
### Result:
IDE internal error occured:
```
Error during dispatching of java.awt.event.MouseEvent[MOUSE_RELEASED,(71,36),absolute(534,685),button=1,modifiers=Button1,clickCount=1] on ###overrideRedirect###
java.lang.NullPointerException
	at net.swengineer.codegraph.graph.presentation.CodeGraphRealizerFactory.setNodeColor(CodeGraphRealizerFactory.java:49)
	at net.swengineer.codegraph.graph.presentation.CodeGraphRealizerFactory.createDefaultNodeRealizer(CodeGraphRealizerFactory.java:31)
	at net.swengineer.codegraph.graph.presentation.CodeGraphPresentationModel.getNodeRealizer(CodeGraphPresentationModel.java:116)
	at net.swengineer.codegraph.graph.presentation.CodeGraphPresentationModel.getNodeRealizer(CodeGraphPresentationModel.java:22)
	at com.intellij.openapi.graph.impl.builder.GraphBuilderImpl.d(GraphBuilderImpl.java:230)
	at com.intellij.openapi.graph.impl.builder.GraphBuilderImpl.c(GraphBuilderImpl.java:215)
	at com.intellij.openapi.graph.impl.builder.GraphBuilderImpl.updateGraph(GraphBuilderImpl.java:42)
	at net.swengineer.codegraph.graph.CodeGraph.updateGraph(CodeGraph.java:119)
	at net.swengineer.codegraph.plugin.actions.AddElementAction.actionPerformed(AddElementAction.java:29)
	at com.intellij.openapi.actionSystem.impl.ActionMenuItem$ActionTransmitter.actionPerformed(ActionMenuItem.java:6)
	at javax.swing.AbstractButton.fireActionPerformed(AbstractButton.java:1995)
	at com.intellij.openapi.actionSystem.impl.ActionMenuItem.fireActionPerformed(ActionMenuItem.java:28)
	at com.intellij.ui.plaf.beg.BegMenuItemUI.a(BegMenuItemUI.java:219)
	at com.intellij.ui.plaf.beg.BegMenuItemUI.access$300(BegMenuItemUI.java:66)
	at com.intellij.ui.plaf.beg.BegMenuItemUI$MyMouseInputHandler.mouseReleased(BegMenuItemUI.java:3)
	at java.awt.Component.processMouseEvent(Component.java:6134)
	at javax.swing.JComponent.processMouseEvent(JComponent.java:3265)
	at java.awt.Component.processEvent(Component.java:5899)
	at java.awt.Container.processEvent(Container.java:2023)
	at java.awt.Component.dispatchEventImpl(Component.java:4501)
	at java.awt.Container.dispatchEventImpl(Container.java:2081)
	at java.awt.Component.dispatchEvent(Component.java:4331)
	at java.awt.LightweightDispatcher.retargetMouseEvent(Container.java:4301)
	at java.awt.LightweightDispatcher.processMouseEvent(Container.java:3965)
	at java.awt.LightweightDispatcher.dispatchEvent(Container.java:3895)
	at java.awt.Container.dispatchEventImpl(Container.java:2067)
	at java.awt.Window.dispatchEventImpl(Window.java:2458)
	at java.awt.Component.dispatchEvent(Component.java:4331)
	at java.awt.EventQueue.dispatchEvent(EventQueue.java:599)
	at com.intellij.ide.IdeEventQueue.c(IdeEventQueue.java:39)
	at com.intellij.ide.IdeEventQueue.b(IdeEventQueue.java:135)
	at com.intellij.ide.IdeEventQueue.dispatchEvent(IdeEventQueue.java:214)
	at java.awt.EventDispatchThread.pumpOneEventForFilters(EventDispatchThread.java:269)
	at java.awt.EventDispatchThread.pumpEventsForFilter(EventDispatchThread.java:184)
	at java.awt.EventDispatchThread.pumpEventsForHierarchy(EventDispatchThread.java:174)
	at java.awt.EventDispatchThread.pumpEvents(EventDispatchThread.java:169)
	at java.awt.EventDispatchThread.pumpEvents(EventDispatchThread.java:161)
	at java.awt.EventDispatchThread.run(EventDispatchThread.java:122)
```
### Expected result:
There are no IDE errors, but it is necessary to provide a warning about the impossibility of performing the action
## 3. The entire project is displayed in CodeGraph. Comment and uncomment part of code (class, method, etc...). Add Entire Project again, the duplicated portion of code will be displayed in CodeGraph.
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
    public void mymethod() {
        System.out.println("My method");
    }  
}
```
- The entire project is displayed in CodeGraph
### STR: 
- 	Change code in "Class1", comment ```mymethod()```:
```
package mypackage;

public class Class1 {
//    public void mymethod() {
//        System.out.println("My method");
//    }  
}
```
-	Change code in "Class1", uncomment ```mymethod()```
```
package mypackage;

public class Class1 {
    public void mymethod() {
        System.out.println("My method");
    }  
}
```
- 	Open the Project tree
-	Place the cursor on package "mypackage"
-	Invoke the context menu by right-clicking
-	Select "CodeGraph" from the context menu
-	Press "Add Entire Project"
### Result:
The method "mymethod" is displayed twice in CodeGraph
### Expected result:
The method "mymethod" is displayed once in CodeGraph
## 4. The entire project is displayed in CodeGraph. Delete some part of code (class, method, etc...). Add Entire Project again, the removed portion of code (class, method, etc...) is still being shown in CodeGraph.
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
    public void mymethod() {
        System.out.println("My method");
    }  
}
```
- The entire project is displayed in CodeGraph
### STR:
- 	Change code in "Class1", delete method ```mymethod()```
- 	Open the Project tree
-	Place the cursor on package "mypackage"
-	Invoke the context menu by right-clicking
-	Select "CodeGraph" from the context menu
-	Press "Add Entire Project"
### Result:
The deleted method (in this example) is still being shown in CodeGraph
### Expected result:
The deleted method (in this example) is not shown in CodeGraph
## 5. Empty classes, interfaces and enum are not displayed in CodeGraph
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
}
```
### STR:
- Open the Project tree
-	Place the cursor on package "mypackage"
-	Invoke the context menu by right-clicking
-	Select "CodeGraph" from the context menu
-	Press "Add Entire Project"
### Result:
An empty class (in this example) is not displayed in CodeGraph
### Expected result:
An empty class (in this example) is displayed in CodeGraph
## 6. The "Refresh" functionality is missing in CodeGraph
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
    public void mymethod() {
        System.out.println("My method");
    }  
}
```
- The entire project is displayed in CodeGraph
### STR:
-	Change code in "Class1", add new ```mymethod1()```
```
package mypackage;

public class Class1 {
    public void mymethod() {
        System.out.println("My method");
    }
    public void mymethod1() {
        System.out.println("My method");
    }   
}
```
### Result:
There are no tools available to refresh the display of new objects in CodeGraph. You can use the "Add Element" feature or add a new method to Class1 through CodeGraph
### Expected result:
I can update the displayed class using the Refresh button in CodeGraph menu
## 7. The "Add field's type" functionality for a field in CodeGraph is not working
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
    private int myField;
    public void mymethod() {
        System.out.println("My method");
    }  
}
```
- The entire project is displayed in CodeGraph
### STR:
- 	Open CodeGraph
- 	Select field myField
-	Invoke the context menu by right-clicking
-	Press "Add field's type"
### Result:
There are no visible changes
### Expected result:
The field type is displayed in CodeGraph
## 8. The interface nested within another interface is not shown through the "Add Interface" option in CodeGraph if the interface is added through the "Add Elements" functionality
### Preconditions:
-	The project contains an interface named "Interface1" and nested interface "InnerInterface1" with the following code:
```
package mypackage;

public interface Interface1 {
    void interfacemethod();
    static interface InnerInterface1{
    void innerinterfacemethod();
    }
}
```
### STR:
- 	Open the Project tree
- 	Select Interface1 in the project tree
-	Invoke the context menu by right-clicking
-	Select "CodeGraph" from the context menu
-	Press "Add Element"
-	Open CodeGraph
-	Select Interface1 in CoedGraph
-	Invoke the context menu by right-clicking
-	Select "Add Interface" option
### Result:
InnerInterface1 is not displayed in CodeGraph
### Expected result:
InnerInterface is contained within Interface1 in CodeGraph
## 9. After closing and reopening the project, CodeGraph does not display the project
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
    public void mymethod1() {
        System.out.println("My method1");
    }
    public void mymethod2() {
        System.out.println("My method2");
    }   
}
```
- The entire project is displayed in CodeGraph
### STR:
- Close IDE by "Close" button
- Open again
- Open CodeGraph
### Result:
CodeGraph does not display the project
### Expected result:
CodeGraph displays the entire project correctly
## 10. It is necessary to add validation for the permissibility of an option in CodeGraph and indicate in gray the elements that are not available
### Preconditions:
-	The project contains a class named "Class1" with the following code:
```
package mypackage;

public class Class1 {
}
```
-	The Class1 is displayed in CodeGraph
### STR:
- 	Open the Project tree
- 	Select Class1 in the project tree
-	Invoke the context menu by right-clicking
-	Select "CodeGraph" from the context menu
### Result:
All options are available for use
### Expected result:
The "Add Element" option should be marked as unavailable since Class1 is already added in CodeGraph
```
P.S.

This is just one example where it would be beneficial to block certain options from the context menu. It is important to conduct further investigation and add checks where necessary to ensure appropriate functionality and restrictions
```
