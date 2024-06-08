### Утиная типизация
collapsed:: true
	-
	-
	- Утиная типизация (duck typing) — это концепция, при которой тип объекта определяется его поведением (методами и свойствами), а не его явной декларацией. Название происходит от фразы "Если это выглядит как утка, плавает как утка и крякает как утка, то это, вероятно, утка".
	  collapsed:: true
	  
	  В языке Go утиная типизация реализуется через интерфейсы. Объект считается соответствующим интерфейсу, если он реализует все методы этого интерфейса, независимо от его явного типа.
		-
	- Например:
		- ```go
		  package main
		  
		  import "fmt"
		  
		  type Quacker interface {
		      Quack()
		  }
		  
		  type Duck struct{}
		  
		  func (d Duck) Quack() {
		      fmt.Println("Quack!")
		  }
		  
		  type Person struct{}
		  
		  func (p Person) Quack() {
		      fmt.Println("I'm quacking like a duck!")
		  }
		  
		  func main() {
		      var q Quacker
		      q = Duck{}
		      q.Quack()
		  
		      q = Person{}
		      q.Quack()
		  }
		  
		  ```
	-
	-
- ### Принцип подстановки Лисков
  collapsed:: true
	- Принцип подстановки Лисков (LSP) является одним из принципов SOLID и гласит, что объекты в программе должны быть заменяемы их подтипами без изменения правильности программы. Это означает, что если у нас есть тип `T` и его подтип `S`, то мы должны иметь возможность использовать объект типа `S` вместо объекта типа `T` без каких-либо негативных последствий.
	- В контексте Go этот принцип также может быть выражен через интерфейсы, но он фокусируется на том, чтобы подтипы (реализации интерфейсов) сохраняли поведение базового типа.
	- Например:
		- ```go
		  package main
		  
		  import "fmt"
		  
		  type Shape interface {
		      Area() float64
		  }
		  
		  type Rectangle struct {
		      Width, Height float64
		  }
		  
		  func (r Rectangle) Area() float64 {
		      return r.Width * r.Height
		  }
		  
		  type Square struct {
		      Side float64
		  }
		  
		  func (s Square) Area() float64 {
		      return s.Side * s.Side
		  }
		  
		  func PrintArea(shape Shape) {
		      fmt.Println("Area:", shape.Area())
		  }
		  
		  func main() {
		      r := Rectangle{Width: 3, Height: 4}
		      s := Square{Side: 5}
		  
		      PrintArea(r)
		      PrintArea(s)
		  }
		  
		  ```
- {{embed [[Отличия:]]}}
- {{embed [[Краткий вывод:]]}}