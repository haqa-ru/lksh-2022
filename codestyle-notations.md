# Рекомендации к кодстайлу

## Основные положения

- Выдержка стиля **_(все должно быть в одном стиле)_**
- Выберите **отступ в 2 или 4 пробела** или **используйте \t** 
> :warning: **_Заметьте, что \t не рекомедуется использовать из-за проблем с отображением в разных редакторах_**.
- Вокруг знаков арифметики, логики и присвоения **ставятся пробелы**.
```c++
+ - / * % > >= == <= < || && | & ^ = += -= /= *= %= |= &= ^= etc.
```
- Унарные операторы **не обособляются**.
```c++
a = -a;
b = !b;
```
- Функции и другие блоки кода **отделяются друг от друга отступами**.
- После запятой **ставится пробел**.
```c++
int a[4] = { 1, 2, 3, 4 };
```
- Между именем _(функции, класса, стуктуры)_ и скобками _(круглыми, треугольными)_ **пробел не ставится**.
```c++
foo();
vector<int>(2, 2);
```
- Каждый новый оператор **находится в отдельной строке**.
- Объявление переменных с присвоением **делается в отдельных строчках**.
```c++
int a = 1;
int b = 2;
```

## Примерный шаблон кода

1. **Подключаемые библиотеки**
2. **Макросы**
3. **Константы**
4. **Свои структуры и классы** 
5. **Глобальные переменные**
6. **Функции**

> _Основной смысл в том, что каждый следующий блок полагается на предыдущий._

## Примеры


```c++
/*
    CodeStyle Example
    It's a multiline comment by the way...
*/

// Applied libraries:

#include <iostream>
#include <vector>

// Macroses:

using namespace std;

// Constants:

const int INF = 1e9;
const long double EXP = 1e-8;
const int MAXN = 1000;

// Custom structs and classes:

struct sample {
    string name;
    int x, y;
    
    sample(string name, int x, int y): name(name), x(x), y(y) {}
};

// Global variables:

bool arr[MAXN];
vector<int> a = { 1, 2, 3, 4, 5 };

// Functions:

int sum(int a, int b) {
    return a + b;
}

int main() {
    freopen("../input.txt", "r", stdin);
    freopen("../output.txt", "w", stdout);
    
    int a, b;
    sample sa("answer", 4, 2);

    cin >> a >> b;

    arr[0] = true;

    for (int i = 1; i < MAXN; i++) {
        if (a < 0 && arr[i - 1]) {
            arr[i] = true;
        }
    }

    for (int i = 0; i < MAXN; i++) {
        arr[i] = false;
    }

    int s = 0;

    if (a < 0) {
        a = -a;
        if (b < 0) {
            b = -b;
            s = a + b;
        }
        else while (s <= 0) {
            switch (a) {
                case 1: {
                    s += 3;
                    break;
                }
                case 2: {
                    s -= 4;
                    a--;
                    break;
                }
            }
        }
    }
    else if (b < 0) {
        b = -b;
        s = (a + b) * (a - b);
    }
    else {
        s = sum(a, b) * sum(a, b);
    }

    cout << s << '\n';

    return 0;
}

```

## Дополнительные ссылки

**[Microsoft Codestyle](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fraw.githubusercontent.com%2Fsphinxlogic%2FAll-In-One-Code-Framework%2Fmaster%2FAll-In-One%2520Code%2520Framework%2520Coding%2520Standards.docx&wdOrigin=BROWSELINK)**

**[Google Codestyle](https://google.github.io/styleguide/cppguide.html)**
