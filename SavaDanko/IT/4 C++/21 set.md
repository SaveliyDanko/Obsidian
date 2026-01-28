[Documentation](https://en.cppreference.com/w/cpp/container/set)
`set` — контейнер предназначенный для хранения уникальных отсортированных элементов. 
```cpp
#include <set>
set<int> mySet;
```

#### ==Часто используемые методы==
`insert(value)` - Вставляет элемент (если его ещё нет)

`earse(value)` - Удаляет элемент

`find(value)` - Возвращает итератор на элемент или `end()`

`count(value)` - 0 или 1 (есть ли элемент в `set`)

`clear` - oчистка всех элементов

`size()` - количество элементов

`begin(), end()` - итераторы на начало и конец

`lower_bound(val)` - Первый элемент не меньше `val`

`upper_bound(val)` - Первый элемент больше `val`

#### ==Кастомный порядок сортировки==
```cpp
std::set<int, std::greater<int>> descSet;  // Сортировка по убыванию
```
