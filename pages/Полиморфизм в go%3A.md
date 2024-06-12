- В языке программирования Go (или Golang) нет традиционного наследования, как в некоторых других объектно-ориентированных языках, таких как Java или Python. Вместо этого **Go использует композицию и интерфейсы для реализации полиморфизма и повторного использования кода**.
	- #+BEGIN_QUOTE
	  Краткий вывод:
	  Полиморфизм — это способность объектов с одинаковой спецификацией проявлять различное поведение.
	  #+END_QUOTE
- ### Пример:
  collapsed:: true
  :LOGBOOK:
  CLOCK: [2024-06-08 Sat 12:12:06]
  :END:
	- ```go
	  package main
	  
	  import "fmt"
	  
	  // Animal - суперкласс (в Go это будет интерфейс)
	  type Animal interface {
	      Speak() string
	  }
	  
	  // Dog - подкласс, который "наследует" от Animal
	  type Dog struct {
	      Name string
	  }
	  
	  // Speak - реализация метода Speak для Dog
	  func (d Dog) Speak() string {
	      return "Woof!"
	  }
	  
	  // Cat - еще один подкласс, который "наследует" от Animal
	  type Cat struct {
	      Name string
	  }
	  
	  // Speak - реализация метода Speak для Cat
	  func (c Cat) Speak() string {
	      return "Meow!"
	  }
	  
	  // main - главная функция программы
	  func main() {
	      // Создаем экземпляры Dog и Cat
	      dog := Dog{Name: "Rex"}
	      cat := Cat{Name: "Whiskers"}
	  
	      // Объявляем переменную типа Animal и присваиваем ей экземпляры Dog и Cat
	      var animal Animal
	  
	      // Присваиваем экземпляр Dog
	      animal = dog
	      fmt.Printf("Dog: %s\n", animal.Speak()) // Выводит: Dog: Woof!
	  
	      // Присваиваем экземпляр Cat
	      animal = cat
	      fmt.Printf("Cat: %s\n", animal.Speak()) // Выводит: Cat: Meow!
	  }
	  
	  ```
	-
- ### Пример 1: Система уведомлений
  collapsed:: true
	- Представьте систему уведомлений, которая может отправлять сообщения через различные каналы (например, электронная почта, SMS, push-уведомления).
	- ```go
	  package main
	  
	  import (
	  	"fmt"
	  )
	  
	  // NotificationSender - интерфейс для отправки уведомлений
	  type NotificationSender interface {
	  	Send(message string) error
	  }
	  
	  // EmailSender - структура для отправки уведомлений по электронной почте
	  type EmailSender struct{}
	  
	  func (e EmailSender) Send(message string) error {
	  	fmt.Println("Sending email:", message)
	  	return nil
	  }
	  
	  // SMSender - структура для отправки SMS
	  type SMSender struct{}
	  
	  func (s SMSender) Send(message string) error {
	  	fmt.Println("Sending SMS:", message)
	  	return nil
	  }
	  
	  // main - функция, демонстрирующая полиморфизм
	  func main() {
	  	senders := []NotificationSender{EmailSender{}, SMSender{}}
	  
	  	for _, sender := range senders {
	  		err := sender.Send("Hello!")
	  		if err!= nil {
	  			fmt.Println(err)
	  		}
	  	}
	  }
	  
	  ```
- ### Пример 2: Работа с файлами
  collapsed:: true
	- Рассмотрим систему, которая может читать и записывать данные в различные форматы файлов.
	- ```go
	  package main
	  
	  import (
	  	"fmt"
	  )
	  
	  // FileHandler - интерфейс для обработки файлов
	  type FileHandler interface {
	  	ReadFile(filename string) ([]byte, error)
	  	WriteFile(filename string, content []byte) error
	  }
	  
	  // TextFileHandler - структура для работы с текстовыми файлами
	  type TextFileHandler struct{}
	  
	  func (t TextFileHandler) ReadFile(filename string) ([]byte, error) {
	  	fmt.Println("Reading text file:", filename)
	  	return []byte("Some text"), nil
	  }
	  
	  func (t TextFileHandler) WriteFile(filename string, content []byte) error {
	  	fmt.Println("Writing to text file:", filename)
	  	return nil
	  }
	  
	  // BinaryFileHandler - структура для работы с бинарными файлами
	  type BinaryFileHandler struct{}
	  
	  func (b BinaryFileHandler) ReadFile(filename string) ([]byte, error) {
	  	fmt.Println("Reading binary file:", filename)
	  	return []byte{0x01, 0x02}, nil
	  }
	  
	  func (b BinaryFileHandler) WriteFile(filename string, content []byte) error {
	  	fmt.Println("Writing to binary file:", filename)
	  	return nil
	  }
	  
	  // main - функция, демонстрирующая полиморфизм
	  func main() {
	  	handlers := []FileHandler{TextFileHandler{}, BinaryFileHandler{}}
	  
	  	for _, handler := range handlers {
	  		content, err := handler.ReadFile("example.txt")
	  		if err!= nil {
	  			fmt.Println(err)
	  		}
	  		fmt.Println(string(content))
	  
	  		err = handler.WriteFile("output.txt", content)
	  		if err!= nil {
	  			fmt.Println(err)
	  		}
	  	}
	  }
	  
	  ```
- ### Объяснение полиморфизма:
- **Интерфейс `Animal`:**
  Интерфейс `Animal` задает контракт: любой тип, который реализует метод `Speak()`, может считаться типом `Animal`.
- **Реализация `Dog` и `Cat`:**
  Структуры `Dog` и `Cat` реализуют метод `Speak()`, что делает их реализациями интерфейса `Animal`.
- **Использование полиморфизма:**
  В функции `main` переменная типа `Animal` сначала содержит объект `Dog`, затем объект `Cat`. В обоих случаях вызывается метод `Speak()`, но результат зависит от конкретной реализации метода в типе (`Dog` или `Cat`).
  
  Это пример полиморфизма, где одна и та же операция (вызов метода `Speak()`) может иметь разные реализации в зависимости от типа объекта, который её выполняет.