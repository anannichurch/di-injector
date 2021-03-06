![technology Go](https://img.shields.io/badge/technology-go-blue.svg)
![goversion-image](https://img.shields.io/badge/Go-1.12+-00ADD8.svg)

# di-injector
di-injector helps you to manage dependency injection.
It works in a very simple way: You just create a DiContainer and add all the dependencies you want to it, finally when 
you are coding your business logic, just mark the struct's fields you want to be injected with the tag: inject:"auto"
and pass this structs to the library to manage the dependencies. The library will look for the "appropriate" dependency
in its bag of dependencies and will inject the value.

### Import Library
```go
package main 
import di_injector "github.com/sebastianMurdoch/di-injector"
```

### Example: Very silly example used just to show you how to use the library
```go
package main

import (
	"fmt"
	di_injector "github.com/sebastianMurdoch/di-injector"
)

func main() {
	/* Create a container */
	c := di_injector.NewDiContainer()
	/* Add your dependencies */
	c.AddToDependencies(" Of course")
	c.AddToDependencies(&ServiceImpl{})
	/* Inject your dependencies */
	bo := businessObject{}
	c.InjectWithDependencies(&bo)
	fmt.Println(bo.SomeService.doService() + bo.CommonString)
}

type businessObject struct {
	CommonString string  `inject:"auto"`
	SomeService  Service `inject:"auto"`
}

type Service interface {
	doService() string
}

type ServiceImpl struct {}

func (s *ServiceImpl) doService() string {
	return "Can this library be more useless?"
}
```
To see a more usefull example please check out this [post](https://medium.com/@sebastianmurdoch12/building-a-golang-development-framework-for-heroku-with-dependency-injection-2e1d3743779e?sk=64b15f4122699eeb386bee305ed34107)

Comments and PRs of any kind are welcome!! Thanks

# Questions?
#### [Sebastian Murdoch](https://github.com/sebastianMurdoch) - sebastianmurdoch12@gmail.com

