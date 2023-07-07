# 1.	Generating code for an empty interface
Preconditions:
-	Project contains file interface.go with following code:
```
package main


type TestedInterface interface {
}
```
-	Project contains file struct.go with following code:
```
Package main


type TestedStruct struct {
}
```
Steps:
-	Select struct name in file struct.go
-	Press Alt+Enter and select “Implement interface”
-	Starts type name of interface TestedInterface and select it
-	Check file struct.go: There are no implemented methods

# 2. Generating code for an interface with 1 method
Preconditions:
-	Project contains file interface.go with following code:
```
package main


type TestedInterface interface {
	SomeMethod()
}
```
-	Project contains file sturct.go with following code:
```
package main


type TestedStruct struct {
}
```
Steps:
-	Select struct name in file struct.go
-	Press Alt+Enter and select “Implement interface”
-	Starts type name of interface TestedInterface and select it
-	Check file struct.go: There is 1 implemeted func exist
```
package main


type TestedStruct struct {
}

func (t TestedStruct) SomeMethod(){
	//TODO implement me
	panic("implement me")
}
```
# 3. Generating code for an interface with > 1 method
Preconditions:
-	Project contains file interface.go with following code:
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
-	Project contains file sturct.go with following code:
```
package main


type TestedStruct struct {
}
```
Steps:
-	Select struct name in file struct.go
-	Press Alt+Enter and select “Implement interface”
-	Starts type name of interface TestedInterface and select it
-	Check file struct.go: There are 2 implemeted func exist
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

# 4. Generating code for an interface with existing methods in a structure
Preconditions:
-	Project contains file interface.go with following code:
```
package main


type TestedInterface interface {
	SomeMethod()
}
```
-	Project contains file sturct.go with following code:
```
package main


type TestedStruct struct {
}

func (t TestedStruct) SomeMethod(){
	//TODO implement me
	panic("implement me")
}
```
Steps:
-	Open file interface.go and add one more method for TestedInterface:
```
package main


type TestedInterface interface {
	SomeMethod()
	SomeMethod2()
}
```
-	Select struct name in file struct.go
-	Press Alt+Enter and select “Implement interface”
-	Starts type name of interface TestedInterface and select it
-	Check file struct.go: There are 2 implemeted func exist
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

# 5. Generating code when implementing an interface with nested interface
Preconditions:
-	Project contains file interface.go with following code:
```
package main


type TestedInterface interface {
	NestedInterface
}

type NestedInterface interface {
	SomeMethod()
}
```
-	Project contains file struct.go with following code:
```
package main


type TestedStruct struct {
}
```
Steps:
-	Select struct name in file struct.go
-	Press Alt+Enter and select “Implement interface”
-	Starts type name of interface TestedInterface and select it
-	Check file struct.go: There is 1 implemeted func exist
```
package main


type TestedStruct struct {
}

func (t TestedStruct) SomeMethod(){
	//TODO implement me
	panic("implement me")
}
```
# 6. Generating code when implementing an interface with methods that have arguments

Preconditions:
-	Project contains file interface.go with following code:
```
package main


type TestedInterface interface {
	MethodWithArgs(arg1 string, arg2 string)
}
```
-	Project contains file struct.go with following code:
```
package main


type TestedStruct struct {
}
```
Steps:
-	Select struct name in file struct.go
-	Press Alt+Enter and select “Implement interface”
-	Starts type name of interface TestedInterface and select it
-	Check file struct.go: There is 1 implemeted func exist
```
package main


type TestedStruct struct {
}

func (t TestedStruct) MethodWithArgs(arg1 string, arg2 string){
	//TODO implement me
	panic("implement me")
}
```
# 7. Generating code when implementing an interface with methods that have arguments of different types

Preconditions:
-	Project contains file interface.go with following code:
```
package main


type TestedInterface interface {
	MethodWithArgs(arg1 string, arg2 int)
}
```
-	Project contains file struct.go with following code:
```
package main


type TestedStruct struct {
}
```
Steps:
-	Select struct name in file struct.go
-	Press Alt+Enter and select “Implement interface”
-	Starts type name of interface TestedInterface and select it
-	Check file struct.go: There is 1 implemeted func exist
```
package main


type TestedStruct struct {
}

func (t TestedStruct) MethodWithArgs(arg1 string, arg2 int){
	//TODO implement me
	panic("implement me")
}
```
# 8. Generating code when implementing an interface with methods that have only argument types

Preconditions:
-	Project contains file interface.go with following code:
```
package main


type TestedInterface interface {
	MethodWithArgs(string, int)
}
```
-	Project contains file struct.go with following code:
```
package main


type TestedStruct struct {
}
```
Steps:
-	Select struct name in file struct.go
-	Press Alt+Enter and select “Implement interface”
-	Starts type name of interface TestedInterface and select it
-	Check file struct.go: There is 1 implemeted func exist
```
package main


type TestedStruct struct {
}

func (t TestedStruct) MethodWithArgs(s string, i int){
	//TODO implement me
	panic("implement me")
}
```
# 9. Test Scenario: Generating code when implementing an interface with methods that return data.

Preconditions:
-	Project contains file interface.go with following code:
```
package main


type TestedInterface interface {
	MethodWithReturn() (arg1 string)
}
```
-	Project contains file struct.go with following code:
```
package main


type TestedStruct struct {
}
```
Steps:
-	Select struct name in file struct.go
-	Press Alt+Enter and select “Implement interface”
-	Starts type name of interface TestedInterface and select it
-	Check file struct.go: There is 1 implemeted func exist
```
package main


type TestedStruct struct {
}

func (t TestedStruct) MethodWithReturn()(arg1 string){
	//TODO implement me
	panic("implement me")
}
```
# 10. Generating code when implementing an interface with methods that return data without specifying arguments.

Preconditions:
-	Project contains file interface.go with following code:
```
package main


type TestedInterface interface {
	MethodWithReturn() (string, int)
}
```
-	Project contains file struct.go with following code:
```
package main


type TestedStruct struct {
}
```
Steps:
-	Select struct name in file struct.go
-	Press Alt+Enter and select “Implement interface”
-	Starts type name of interface TestedInterface and select it
-	Check file struct.go: There is 1 implemeted func exist
```
package main


type TestedStruct struct {
}

func (t TestedStruct) MethodWithArgs() (string, int) {
	//TODO implement me
	panic("implement me")
}
```

# 11. Generating code when implementing an interface with methods that return data with different types

Preconditions:
-	Project contains file interface.go with following code:
```
package main


type TestedInterface interface {
	MethodWithReturn() (arg1 string, arg2 int)
}
```
-	Project contains file struct.go with following code:
```
package main


type TestedStruct struct {
}
```
Steps:
-	Select struct name in file struct.go
-	Press Alt+Enter and select “Implement interface”
-	Starts type name of interface TestedInterface and select it
-	Check file struct.go: There is 1 implemeted func exist
```
package main


type TestedStruct struct {
}

func (t TestedStruct) MethodWithArgs()(arg1 string, arg2 int){
	//TODO implement me
	panic("implement me")
}
```

# 12. Generating code for multiple interface implementation

Preconditions:
-	Project contains file interface.go with following code:
```
package main


type TestedInterface1 interface {
	Method1()
}

type TestedInterface2 interface {
	Method2()
}
```
-	Project contains file struct.go with following code:
```
package main


type TestedStruct struct {
}
```
Steps:
-	Select struct name in file struct.go
-	Press Alt+Enter and select “Implement interface”
-	Starts type name of interface TestedInterface1 and select it
-	Check file struct.go: There is 1 implemeted func exist
```
package main


type TestedStruct struct {
}

func (t TestedStruct) Method1(){
	//TODO implement me
	panic("implement me")
}
```
- Select struct name in file struct.go
- Press Alt+Enter and select "Implement interface"
- Start type name of Interface TestedInterface2 and select it
- Check file struct.go There is 2 implemented func exist
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

# 13. Generating code when implementing an interface with methods that have nested structs as arguments:
Preconditions:
-	Project contains file interface.go with following code:
```
package main


type TestedInterface interface {
	Method1(arg NestedStruct)
}

type NestedStruct struct {
	Value int
}
```
-	Project contains file struct.go with following code:
```
package main


type TestedStruct struct {
}
```
Steps:
-	Select struct name in file struct.go
-	Press Alt+Enter and select “Implement interface”
-	Starts type name of interface TestedInterface and select it
-	Check file struct.go: There is 1 implemeted func exist
```
package main


type TestedStruct struct {
}

func (t TestedStruct) Method1(arg NestedStruct){
	//TODO implement me
	panic("implement me")
}
```
# 14. Generating code for an interface with methods having variadic arguments

Preconditions:
-	Project contains file interface.go with following code:
```
package main


type TestedInterface interface {
	MethodWithReturn(args ...int)
}
```
-	Project contains file struct.go with following code:
```
package main


type TestedStruct struct {
}
```
Steps:
-	Select struct name in file struct.go
-	Press Alt+Enter and select “Implement interface”
-	Starts type name of interface TestedInterface and select it
-	Check file struct.go: There is 1 implemeted func exist
```
package main


type TestedStruct struct {
}

func (t TestedStruct) MethodWithReturn(args ...int){
	//TODO implement me
	panic("implement me")
}
```
# 15. Generating code for an interface with an embedded type

Preconditions:
-	Project contains file interface.go with following code:
```
package main


type TestedInterface interface {
	Method1() string
}
```
-	Project contains file struct.go with following code:
```
package main


type TestedStruct struct {
}
```
Steps:
-	Select struct name in file struct.go
-	Press Alt+Enter and select “Implement interface”
-	Starts type name of interface TestedInterface and select it
-	Check file struct.go: There is 1 implemeted func exist
```
package main


type TestedStruct struct {
}

func (t TestedStruct) Method1() string{
	//TODO implement me
	panic("implement me")
}
```
