#### Определение и инициализация карт

Карты в Go определяются с помощью ключевого слова `map`, после которого указываются типы ключей и значений. Карты можно инициализировать несколькими способами:
- **Использование встроенной функции `make`:**
- ```go
  m := make(map[string]int)
  ```
- **Инициализация с литералом карты:**
- ```go
  m := map[string]int{
    "Alice": 25,
    "Bob": 30,
  }
  ```
- ### Основные операции с картами
- #### Вставка и обновление значений
  
  Значения добавляются или обновляются в карте с использованием синтаксиса `map[key] = value`:
  
  ```go
  package main
  
  import "fmt"
  
  func main() {
    m := make(map[string]int)
    
    // Вставка значений
    m["Alice"] = 25
    m["Bob"] = 30
    
    // Обновление значения
    m["Alice"] = 26
    
    fmt.Println(m) // Output: map[Alice:26 Bob:30]
  }
  ```
- #### Доступ к значениям
  
  Для доступа к значениям используется синтаксис `map[key]`. Если ключ не найден, возвращается нулевое значение для типа значений карты:
  
  ```go
  package main
  
  import "fmt"
  
  func main() {
    m := map[string]int{
        "Alice": 25,
        "Bob": 30,
    }
    
    age := m["Alice"]
    fmt.Println(age) // Output: 25
    
    age = m["Charlie"]
    fmt.Println(age) // Output: 0 (ключ не найден)
  }
  ```
- #### Проверка наличия ключа
  
  Для проверки наличия ключа в карте используется двойное присваивание. Второе возвращаемое значение указывает, присутствует ли ключ в карте:
  
  ```go
  package main
  
  import "fmt"
  
  func main() {
    m := map[string]int{
        "Alice": 25,
        "Bob": 30,
    }
    
    age, exists := m["Alice"]
    if exists {
        fmt.Println("Alice is", age) // Output: Alice is 25
    } else {
        fmt.Println("Alice not found")
    }
    
    age, exists = m["Charlie"]
    if !exists {
        fmt.Println("Charlie not found") // Output: Charlie not found
    }
  }
  ```
- #### Удаление ключа
  
  Ключ и его значение удаляются из карты с помощью функции `delete`:
  
  ```go
  package main
  
  import "fmt"
  
  func main() {
    m := map[string]int{
        "Alice": 25,
        "Bob": 30,
    }
    
    delete(m, "Alice")
    
    fmt.Println(m) // Output: map[Bob:30]
  }
  ```
- #### Итерация по карте
  
  Для перебора всех ключей и значений карты используется цикл `for range`:
  
  ```go
  package main
  
  import "fmt"
  
  func main() {
    m := map[string]int{
        "Alice": 25,
        "Bob": 30,
        "Charlie": 35,
    }
    
    for key, value := range m {
        fmt.Printf("%s is %d years old\n", key, value)
    }
  }
  ```
- ### Применение карт в реальных приложениях
- #### Пример: Подсчет количества слов в тексте
  
  Рассмотрим пример, где используется карта для подсчета частоты встречаемости слов в тексте:
  
  ```go
  package main
  
  import (
    "fmt"
    "strings"
  )
  
  func main() {
    text := "hello world hello Go"
    words := strings.Fields(text)
    
    wordCount := make(map[string]int)
    
    for _, word := range words {
        wordCount[word]++
    }
    
    for word, count := range wordCount {
        fmt.Printf("%s: %d\n", word, count)
    }
  }
  ```
  
  В этом примере:
- Текст разбивается на слова с использованием функции `strings.Fields`.
- Карта `wordCount` используется для подсчета количества вхождений каждого слова.
- ### Композиция структур и карт
  
  Карты часто используются в сочетании с другими структурами данных, такими как структуры, для создания сложных моделей данных.
- #### Пример: Управление библиотекой книг
  
  ```go
  package main
  
  import "fmt"
  
  type Book struct {
    Title  string
    Author string
  }
  
  func main() {
    library := make(map[string]Book)
    
    library["978-0140449136"] = Book{Title: "The Republic", Author: "Plato"}
    library["978-0486278070"] = Book{Title: "Meditations", Author: "Marcus Aurelius"}
    
    for isbn, book := range library {
        fmt.Printf("ISBN: %s, Title: %s, Author: %s\n", isbn, book.Title, book.Author)
    }
  }
  ```
  
  В этом примере:
- Карта `library` использует ISBN книги в качестве ключа и структуру `Book` в качестве значения.
- Итерация по карте позволяет вывести информацию о каждой книге в библиотеке.
- ### Заключение
  
  Карты в Go предоставляют мощный и гибкий инструмент для работы с ассоциативными массивами, позволяя быстро и эффективно управлять парами ключ-значение. Они особенно полезны для задач, связанных с поиском и хранением данных, требующих быстрого доступа по ключам.