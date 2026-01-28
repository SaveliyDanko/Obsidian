В C++ `stack` — это контейнер из стандартной библиотеки, представляющий структуру данных **LIFO (Last In, First Out)**. 

#### <mark style="background: #ABF7F7A6;">1. Подключение и объявление</mark>
Для использования `stack` необходимо подключить заголовочный файл:
```cpp
#include <stack>
```

Объявление стека:
```cpp
stack<int> myStack;
```

#### <mark style="background: #ABF7F7A6;">2. Основные операции</mark>
Методы, которые предоставляет `std::stack`:

| Метод         | Описание                                               |
| ------------- | ------------------------------------------------------ |
| `push(value)` | Добавляет элемент `value` на вершину стека             |
| `pop()`       | Удаляет верхний элемент (без его возврата)             |
| `top()`       | Возвращает ссылку на верхний элемент                   |
| `empty()`     | Проверяет, пуст ли стек (возвращает `true`, если пуст) |
| `size()`      | Возвращает количество элементов в стеке                |

#### <mark style="background: #ABF7F7A6;">3. Пример использования</mark>
```cpp
#include <iostream>
#include <stack>
using namespace std;

int main() {
    stack<int> s;
	
    s.push(10);  // Добавляем элементы
    s.push(20);
    s.push(30);
	
    cout << "Top element: " << s.top() << "\n"; // 30
	
    s.pop(); // Удаляем верхний элемент
	
    cout << "New top element: " << s.top() << "\n"; // 20
	
    cout << "Stack size: " << s.size() << "\n"; // 2
	
    return 0;
}
```
