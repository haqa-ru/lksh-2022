# Рекомендации к кодстайлу

## Основные положения

- Выдержка стиля **_(все должно быть в одном стиле)_**
- Выберите **отступ в 2 или 4 пробела** или **используйте \t**

> :warning: _Заметьте, что **\t** не рекомедуется использовать из-за проблем с отображением в разных редакторах_.

- Длина строки в коде **должна быть ограничена.** _(обычно <= 100 символов)_
- Транслит **категорически запрещён**
- Названия **должны быть осмысленные**
- Названия констант пишутся **БОЛЬШИМИ БУКВАМИ**

## Форматирование

- Вокруг знаков арифметики, логики и присвоения **ставятся пробелы**

```c++
+ - / * % > >= == <= < || && | & ^ = += -= /= *= %= |= &= ^= etc.
```

- Унарные операторы и разыменование **не обособляются**

```c++
a = -a;
b = !b;
a_ptr = &a;
c = *a_ptr; 
obj_field = obj->field;
```

- Блоки кода **отделяются пробелом и отступом**

```c++
class {
    // Может быть телом класса/структуры,
};

void fn(...) {
    // функции
}

{
    // или блоком.
}
```

- После запятой **ставится пробел**.

```c++
int a[4] = { 1, 2, 3, 4 };
```

- Между именем _(функции, класса, стуктуры)_ и скобками _(круглыми, треугольными)_ **пробел не ставится**

```c++
foo();
vector<int>(2, 2);
```

- Определение переменных

```c++
int a = 1;
int b = 2;
int c, d;
vector<int> e;
```

- Переносы

```c++
int len = abs(a * x + b * y + c)
    / sqrtl(a * a + b * b);

int very_long_function_name(int even_bigger_parameter_name, int not_so_big_one,
                            int i_fell_off, int just_d) {}

int result = very_long_function_name(
    passing_even_bigger_parameter, and_not_so_big_one,
    it_fell_off, d);
```

- Базовые конструкции

```c++
if (very_very_long_condition_you_should_care_about
    && i_fell_off_again) {
    // Если то - я. 
}
else if (...) {
    // Иначе если - я.
}
else {
    // Ну или - я.
}

for (...) {
    // Делаю что-то, сколько-то...
}

do {
    // Сделаю хотя-бы раз.
} while ((with && greater && priority) || (still && scoped));
```

## Примерный шаблон кода

1. **Подключаемые библиотеки**
2. **Макросы**
3. **Константы**
4. **Свои структуры/классы**
5. **Глобальные переменные**
6. **Функции**

> :weary: _Основной смысл в том, что каждый следующий блок полагается на предыдущий._

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
    freopen("input.txt", "r", stdin);
    freopen("output.txt", "w", stdout);
    
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

> :hearts: **Существуют и другие стили, которые вы можете свободно эксплуатировать!**

**[Microsoft Codestyle](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fraw.githubusercontent.com%2Fhaqa-ru%2Flksh-2022%2Fmain%2FAll-In-One%2520Code%2520Framework%2520Coding%2520Standards.docx&wdOrigin=BROWSELINK)**

**[Google Codestyle](https://google.github.io/styleguide/cppguide.html)**
