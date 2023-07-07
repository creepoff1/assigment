
# This test plan contains test cases for verifying the functionality of the "Implement interface" feature in GoLand IDE. The focus here is on testing positive scenarios, following the available documentation for the feature.

## 1.	Generating code for an empty interface
### Preconditions:
-	The project contains a file named interface.go with the following code:
```
package main


type TestedInterface interface {
}
```
-	The project contains a file named struct.go with the following code:
```
Package main


type TestedStruct struct {
}
```
### Steps:
-	Open the struct.go file for editing
-	Place the cursor on the name of the structure TestedStruct
-	Press Alt+Enter to invoke the context menu and double-click on the "Implement interface" option
-	Start typing the name of the interface "TestedInterface"
-	Double-click on the TestedInterface interface to select it
### Result:
-	Сheck the struct.go file: No functions were implemented (the interface is empty)
## 2. Generating code for an interface with one method
### Preconditions:
-	The project contains a file named interface.go with the following code:
```
package main


type TestedInterface interface {
	SomeMethod()
}
```
-	The project contains a file named struct.go with the following code:
```
package main


type TestedStruct struct {
}
```
### Steps:
-	Open the struct.go file for editing
-	Place the cursor on the name of the structure TestedStruct
-	Press Alt+Enter to invoke the context menu and double-click on the "Implement interface" option
-	Start typing the name of the interface "TestedInterface"
-	Double-click on the TestedInterface interface to select it
  ### Result:
-	Сheck the struct.go file: One function has been implemented for the interface method
```
package main


type TestedStruct struct {
}

func (t TestedStruct) SomeMethod(){
	//TODO implement me
	panic("implement me")
}
```
## 3. Generating code for an interface with more than one method
### Preconditions:
-	The project contains a file named interface.go with the following code:
```
package main


type TestedInterface interface {
	SomeMethod1()
	SomeMethod2()
	.
	.
	.
	SomeMethodN()
}
```
-	The project contains a file named struct.go with the following code:
```
package main


type TestedStruct struct {
}
```
### Steps:
-	Open the struct.go file for editing
-	Place the cursor on the name of the structure TestedStruct
-	Press Alt+Enter to invoke the context menu and double-click on the "Implement interface" option
-	Start typing the name of the interface "TestedInterface"
-	Double-click on the TestedInterface interface to select it
### Result:
-	Сheck the struct.go file: Functions have been implemented for all interface methods
```
package main


type TestedStruct struct {
}

func (t TestedStruct) SomeMethod1(){
	//TODO implement me
	panic("implement me")
}

func (t TestedStruct) SomeMethod2(){
	//TODO implement me
	panic("implement me")
}

.
.
.

func (t TestedStruct) SomeMethodN(){
	//TODO implement me
	panic("implement me")
}
```

## 4. Generating code for a new method in the interface
### Preconditions:
-	The project contains a file named interface.go with the following code:
```
package main


type TestedInterface interface {
	SomeMethod()
}
```
-	The project contains a file named struct.go with the following code:
```
package main


type TestedStruct struct {
}

func (t TestedStruct) SomeMethod(){
	//TODO implement me
	panic("implement me")
}
```
### Steps:
-	Open the interface.go file and add a new method to the TestedInterface:
```
package main


type TestedInterface interface {
	SomeMethod()
	SomeMethod2()
}
```
-	Open the struct.go file for editing
-	Place the cursor on the name of the structure TestedStruct
-	Press Alt+Enter to invoke the context menu and double-click on the "Implement interface" option
-	Start typing the name of the interface "TestedInterface"
-	Double-click on the TestedInterface interface to select it
### Result:
-	Сheck the struct.go file: A function has been implemented for the new interface method, and the file contains two unique functions
```
package main


type TestedStruct struct {
}

func (t TestedStruct) SomeMethod(){
	//TODO implement me
	panic("implement me")
}

func (t TestedStruct) SomeMethod2(){
	//TODO implement me
	panic("implement me")
}
```

## 5. Generating code for an interface that contains a call to a nested interface.
### Preconditions:
-	The project contains a file named interface.go with the following code:
```
package main


type TestedInterface interface {
	CalledInterface
}

type CalledInterface interface {
	SomeMethod()
}
```
-	The project contains a file named struct.go with the following code:
```
package main


type TestedStruct struct {
}
```
### Steps:
-	Open the struct.go file for editing
-	Place the cursor on the name of the structure TestedStruct
-	Press Alt+Enter to invoke the context menu and double-click on the "Implement interface" option
-	Start typing the name of the interface "TestedInterface"
-	Double-click on the TestedInterface interface to select it
### Result:
-	Сheck the struct.go file: One function has been implemented for the interface method
```
package main


type TestedStruct struct {
}

func (t TestedStruct) SomeMethod(){
	//TODO implement me
	panic("implement me")
}
```
## 6. Generating code for implementing an interface whose methods have arguments

### Preconditions:
-	The project contains a file named interface.go with the following code:
```
package main


type TestedInterface interface {
	MethodWithArgs(arg1 string, arg2 string)
}
```
-	The project contains a file named struct.go with the following code:
```
package main


type TestedStruct struct {
}
```
### Steps:
-	Open the struct.go file for editing
-	Place the cursor on the name of the structure TestedStruct
-	Press Alt+Enter to invoke the context menu and double-click on the "Implement interface" option
-	Start typing the name of the interface "TestedInterface"
-	Double-click on the TestedInterface interface to select it
### Result:
-	Сheck the struct.go file: One function has been implemented for the interface method
```
package main


type TestedStruct struct {
}

func (t TestedStruct) MethodWithArgs(arg1 string, arg2 string){
	//TODO implement me
	panic("implement me")
}
```
## 7. Generating code for implementing an interface with methods that have arguments of different data types
### Preconditions:
-	The project contains a file named interface.go with the following code:
```
package main


type TestedInterface interface {
	MethodWithArgs(arg1 string, arg2 int)
}
```
-	The project contains a file named struct.go with the following code:
```
package main


type TestedStruct struct {
}
```
### Steps:
-	Open the struct.go file for editing
-	Place the cursor on the name of the structure TestedStruct
-	Press Alt+Enter to invoke the context menu and double-click on the "Implement interface" option
-	Start typing the name of the interface "TestedInterface"
-	Double-click on the TestedInterface interface to select it
### Result:
-	Сheck the struct.go file: One function has been implemented for the interface method
```
package main


type TestedStruct struct {
}

func (t TestedStruct) MethodWithArgs(arg1 string, arg2 int){
	//TODO implement me
	panic("implement me")
}
```
## 8. Generating code for implementing an interface whose methods have arguments with only data types specified
### Preconditions:
-	The project contains a file named interface.go with the following code:
```
package main


type TestedInterface interface {
	MethodWithArgs(string, int)
}
```
-	The project contains a file named struct.go with the following code:
```
package main


type TestedStruct struct {
}
```
### Steps:
-	Open the struct.go file for editing
-	Place the cursor on the name of the structure TestedStruct
-	Press Alt+Enter to invoke the context menu and double-click on the "Implement interface" option
-	Start typing the name of the interface "TestedInterface"
-	Double-click on the TestedInterface interface to select it
### Result:
-	Сheck the struct.go file: One function has been implemented for the interface method
```
package main


type TestedStruct struct {
}

func (t TestedStruct) MethodWithArgs(s string, i int){
	//TODO implement me
	panic("implement me")
}
```
## 9. Generating code for an interface that contains methods with return values
### Preconditions:
-	The project contains a file named interface.go with the following code:
```
package main


type TestedInterface interface {
	MethodWithReturn() (arg1 string)
}
```
-	The project contains a file named struct.go with the following code:
```
package main


type TestedStruct struct {
}
```
### Steps:
-	Open the struct.go file for editing
-	Place the cursor on the name of the structure TestedStruct
-	Press Alt+Enter to invoke the context menu and double-click on the "Implement interface" option
-	Start typing the name of the interface "TestedInterface"
-	Double-click on the TestedInterface interface to select it
### Result:
-	Сheck the struct.go file: One function has been implemented for the interface method
```
package main


type TestedStruct struct {
}

func (t TestedStruct) MethodWithReturn()(arg1 string){
	//TODO implement me
	panic("implement me")
}
```
## 10. Generating code for an interface where the methods return data without declaring arguments
### Preconditions:
-	The project contains a file named interface.go with the following code:
```
package main


type TestedInterface interface {
	MethodWithReturn() (string, int)
}
```
-	The project contains a file named struct.go with the following code:
```
package main


type TestedStruct struct {
}
```
### Steps:
-	Open the struct.go file for editing
-	Place the cursor on the name of the structure TestedStruct
-	Press Alt+Enter to invoke the context menu and double-click on the "Implement interface" option
-	Start typing the name of the interface "TestedInterface"
-	Double-click on the TestedInterface interface to select it
### Result:
-	Сheck the struct.go file: One function has been implemented for the interface method
```
package main


type TestedStruct struct {
}

func (t TestedStruct) MethodWithArgs() (string, int) {
	//TODO implement me
	panic("implement me")
}
```

## 11. Generating code for an interface where the methods return data with different types
### Preconditions:
-	The project contains a file named interface.go with the following code:
```
package main


type TestedInterface interface {
	MethodWithReturn() (arg1 string, arg2 int)
}
```
-	The project contains a file named struct.go with the following code:
```
package main


type TestedStruct struct {
}
```
### Steps:
-	Open the struct.go file for editing
-	Place the cursor on the name of the structure TestedStruct
-	Press Alt+Enter to invoke the context menu and double-click on the "Implement interface" option
-	Start typing the name of the interface "TestedInterface"
-	Double-click on the TestedInterface interface to select it
### Result:
-	Сheck the struct.go file: One function has been implemented for the interface method
```
package main


type TestedStruct struct {
}

func (t TestedStruct) MethodWithArgs()(arg1 string, arg2 int){
	//TODO implement me
	panic("implement me")
}
```

## 12. Generating code for multiple interfaces
### Preconditions:
-	The project contains a file named interface.go with the following code:
```
package main


type TestedInterface1 interface {
	Method1()
}

type TestedInterface2 interface {
	Method2()
}
```
-	The project contains a file named struct.go with the following code:
```
package main


type TestedStruct struct {
}
```
### Steps:
-	Open the struct.go file for editing
-	Place the cursor on the name of the structure TestedStruct
-	Press Alt+Enter to invoke the context menu and double-click on the "Implement interface" option
-	Start typing the name of the interface "TestedInterface1"
-	Double-click on the TestedInterface1 interface to select it
```
package main


type TestedStruct struct {
}

func (t TestedStruct) Method1(){
	//TODO implement me
	panic("implement me")
}
```
-	Open the struct.go file for editing
-	Place the cursor on the name of the structure TestedStruct
-	Press Alt+Enter to invoke the context menu and double-click on the "Implement interface" option
-	Start typing the name of the interface "TestedInterface2"
-	Double-click on the TestedInterface2 interface to select it
### Result:
- 	Check the struct.go file. Two functions have been implemented for the methods of two interfaces.
```
package main


type TestedStruct struct {
}

func (t TestedStruct) Method1(){
	//TODO implement me
	panic("implement me")
}

func (t TestedStruct) Method2(){
	//TODO implement me
	panic("implement me")
}
```

## 13. Generating code for an interface whose methods have calls to structures in the arguments
### Preconditions:
-	The project contains a file named interface.go with the following code:
```
package main


type TestedInterface interface {
	Method1(arg NestedStruct)
}

type NestedStruct struct {
	Value int
}
```
-	The project contains a file named struct.go with the following code:
```
package main


type TestedStruct struct {
}
```
### Steps:
-	Open the struct.go file for editing
-	Place the cursor on the name of the structure TestedStruct
-	Press Alt+Enter to invoke the context menu and double-click on the "Implement interface" option
-	Start typing the name of the interface "TestedInterface"
-	Double-click on the TestedInterface interface to select it
### Result:
-	Сheck the struct.go file: One function has been implemented for the interface method
```
package main


type TestedStruct struct {
}

func (t TestedStruct) Method1(arg NestedStruct){
	//TODO implement me
	panic("implement me")
}
```
## 14. Generating code for an interface whose methods have variadic arguments
### Preconditions:
-	The project contains a file named interface.go with the following code:
```
package main


type TestedInterface interface {
	MethodWithReturn(args ...int)
}
```
-	The project contains a file named struct.go with the following code:
```
package main


type TestedStruct struct {
}
```
### Steps:
-	Open the struct.go file for editing
-	Place the cursor on the name of the structure TestedStruct
-	Press Alt+Enter to invoke the context menu and double-click on the "Implement interface" option
-	Start typing the name of the interface "TestedInterface"
-	Double-click on the TestedInterface interface to select it
### Result:
-	Сheck the struct.go file: One function has been implemented for the interface method
```
package main


type TestedStruct struct {
}

func (t TestedStruct) MethodWithReturn(args ...int){
	//TODO implement me
	panic("implement me")
}
```
