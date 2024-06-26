- Пункты:
- Есть интерфейс
  logseq.order-list-type:: number
- Если структура реализует метод из этого интерфеса
  logseq.order-list-type:: number
- То тип интерфейса имеет доступ до этой структуры
  logseq.order-list-type:: number
- ```go
  package main
  
  import "fmt"
  
  // Интерфейс Shape для геометрических фигур
  type Shape interface {
  	Area() float64
  	Perimeter() float64
  }
  
  type Circle struct {
  	Radius float64
  }
  
  func (c Circle) Area() float64 {
  	return 3.14 * c.Radius * c.Radius
  }
  
  func (c Circle) Perimeter() float64 {
  	return 2 * 3.14 * c.Radius
  }
  
  // Структура Rectangle представляет прямоугольник с высотой и шириной
  type Rectangle struct {
  	Width  float64
  	Height float64
  }
  
  // Методы для вычисления площади и периметра прямоугольника
  func (r Rectangle) Area() float64 {
  	return r.Width * r.Height
  }
  
  func (r Rectangle) Perimeter() float64 {
  	return 2 * (r.Width + r.Height)
  }
  
  //! ВНИМАНИЕ Использование интерфейса Shape:
  
  // Функция для вывода площади и периметра фигуры
  func PrintShapeDetails(s Shape) {
  	fmt.Printf("Area: %.2f\n", s.Area())
  	fmt.Printf("Perimeter: %.2f\n", s.Perimeter())
  }
  
  func main() {
  	// Создаем экземпляры круга и прямоугольника
  	circle := Circle{Radius: 5}
  	rectangle := Rectangle{Width: 3, Height: 4}
  
  	// Вызываем функцию для вывода деталей каждой фигуры
  	fmt.Println("Circle details:")
  	PrintShapeDetails(circle)
  	fmt.Println("\nRectangle details:")
  	PrintShapeDetails(rectangle)
  }
   
  ```
	- Или другая задача
	- передавать нужно структуру в которой есть тип интерфес
- ```go
  package main
  
  import "fmt"
  
  // Интерфейс Printer с методом Print
  type Printer interface {
      Print() string
  }
  // Структура Document представляет документ с текстом
  type Document struct {
      Text string
  }
  
  // Реализация метода Print для структуры Document
  func (d Document) Print() string {
      return "Document: " + d.Text
  }
  
  // Структура Photo представляет фотографию с названием
  type Photo struct {
      Title string
  }
  
  // Реализация метода Print для структуры Photo
  func (p Photo) Print() string {
      return "Photo: " + p.Title
  }
  // Функция для печати деталей
  func PrintDetails(p Printer) {
      fmt.Println(p.Print())
  }
  
  func main() {
      // Создаем экземпляры Document и Photo
      doc := Document{Text: "This is a document"}
      photo := Photo{Title: "A beautiful sunset"}
  
      // Вызываем функцию для печати деталей каждой структуры
      PrintDetails(doc)
      PrintDetails(photo)
  }
  
  ```
	- Или другая задача
- ```go
  package main
  
  import "fmt"
  
  type Printer struct {
  	Text string
  }
  
  type Contract interface {
  	GetText() string
  }
  
  func (p *Printer) GetText() string {
  	return "Text " + p.Text
  }
  
  
  func DataGet(c Contract){
  	fmt.Println(c.GetText())
  }
  
  func main() {
  	text := &Printer{Text: "OK"}
  	DataGet(text)
  
  }
  
  ```