**Подключаем библиотеку**
```cpp
#include <fstream>
```

#### <mark style="background: #ABF7F7A6;">Чтение из файла (ifstream)</mark>
```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
    ifstream file("input.txt"); // открыть файл для чтения
	
    if (!file) {
        cout << "Не удалось открыть файл.\n";
        return 1;
    }
	
    string line;
    while (getline(file, line)) {
        cout << line << endl;
    }
	
    file.close(); // необязательно: закроется автоматически
    return 0;
}
```

#### <mark style="background: #ABF7F7A6;">Запись в файл (ofstream)</mark>
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    ofstream file("output.txt"); // открыть файл для записи (перезапишет, если уже есть)
	
    if (!file) {
        cout << "Ошибка открытия файла для записи.\n";
        return 1;
    }
	
    file << "Привет, файл!" << endl;
    file << 42 << " — это число." << endl;
	
    file.close();
    return 0;
}
```

> Если хочешь **дописать** в файл (не затирать), нужно открыть его с флагом `ios::app`:
```cpp
ofstream file("output.txt", ios::app); // дописать в конец файла
```


#### <mark style="background: #ABF7F7A6;">Чтение и запись (fstream)</mark>
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    fstream file("data.txt", ios::in | ios::out); // открыть и для чтения, и для записи

    if (!file) {
        cout << "Не удалось открыть файл.\n";
        return 1;
    }

    string word;
    file >> word;
    cout << "Первое слово в файле: " << word << endl;

    file.seekp(0, ios::end); // переместить указатель записи в конец
    file << "\nНовое добавление.";

    file.close();
    return 0;
}
```