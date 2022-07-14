# Лекция 1 - Базовые структуры данных
ЛКШ.Ставрополь | Параллель С


## Правильная скобочная последовательность
Представим следующую задачу - у нас есть последовательность, которая состоит из открывающихся и закрывающихся круглых скобок. Нужно определить, является ли данная скобочная последовательность правильной. 

***Правильная скобочная последовательность (ПСП)*** – это та, которая может получиться в результате удаления из какого-либо арифметического выражения всех символов кроме скобок. 

> Пример: корректные – (()), ()(), (()()), некорректные - )(, ((), (()))

Со временем можно прийти к выводу, что если скобочная последовательность правильная, то перед каждой закрывающейся скобкой должна быть хотя бы одна открывающаяся.

Тогда решение простое - держим счётчик открытых скобок, если встречаем `(`, то прибавляем 1, иначе вычитаем 1. Если счётчик всегда больше нуля, то перед нами ПСП.

Но что делать, если могут быть не только круглые скобки, но и фигурные? А если ещё и квадратные? Здесь нам поможет стек.

## Стек

***Стек*** – структура данных, в которой элемент, который добавляется последним, удаляется первым. Для сравнения можно представить очень узкую банку с шариками, и чтобы достать шарик на дне, надо достать все шарики, которые выше него:

![Пример стека](https://sun9-50.userapi.com/impf/qx5S1Q589S7UTV1gh7NOFYJElHm7bbmaSLa9oQ/VXHk9fk3weY.jpg?size=551x388&quality=96&sign=c10ef22e5f53722a352d8f79d7d62ddd&type=album)

В этой структуре поддерживается всего 3 операции:
1. `pop` - убрать элемент, который находится сверху стека
2. `push` - положить новый элемент наверх стека
3. `top` - получить верхний элемент стека.

Все три операции реализуются очень просто. Для реализации стека нам необходим счётчик, который будет отражать сколько элементов сейчас в стеке, и массив, в котором будут храниться наши элементы.
Тогда
### Push
```Pascal
function push(x: integer)
begin
    st[sz] := x;
    sz := sz + 1;
end
```

### Pop
```Pascal
function pop()
begin
    if (sz != 0) then
        sz := sz - 1;
end
```

### Top
```Pascal
integer top()
begin
    if (sz != 0) then
        return st[sz - 1];
    else
        return -1; //НЕТ ПОДХОДЯЩЕГО ЭЛЕМЕНТА
end
```

Вернёмся к задаче о скобочных последовательностях - пусть теперь будут не только круглые, но ещё и квадратные и фигурные. Тогда прошлое решение с счётчиком не подойдёт - последовательность `(][)` в таком случае посчитается за правильную, а это не так.

Теперь не трудно заметить, что закрывающаяся скобка всегда открывает последнюю ещё не закрытую скобку подходящего вида, тогда давайте хранить все *пока ещё* открытые скобки в стеке. Если последняя открытая скобка не совпадает по типу с закрывающей скобкой, которую мы смотрим сейчас, то последовательность неправильная. Дополнительно необходимо учитывать моменты, когда у нас нет открытых скобок - в этом случае последовательность также неправильная.

## Очередь

***Очередь (англ. queue)***  — это структура данных, добавление и удаление элементов в которой происходит путём операций push и pop соответственно. Притом первым из очереди удаляется элемент, который был помещен туда первым, то есть в очереди реализуется принцип «первым вошел — первым вышел» (англ. first-in, first-out — FIFO).

![Очередь](https://neerc.ifmo.ru/wiki/images/thumb/c/c1/Fifo_new.png/150px-Fifo_new.png)

Очередь поддерживает те же операции, что и стек:
1. `pop` - убрать элемент из очереди
2. `push` - положить элемент в очередь
3. `front` - получить первый в очереди элемент

Для реализации очереди вместительностью `n` потребуется массив размера как минимум `n`, указатель на начало очереди - head (голова) и указатель на конец очереди - tail (хвост). Когда элемент ставится в очередь, он занимает место в её хвосте. Из очереди всегда выводится элемент, который находится в ее голове.

### Empty
```Pascal
boolean empty()
begin
    return head == tail;
end
```

### Push
```Pascal
function push(x: integer)
begin
    elements[tail] := x
    tail := (tail + 1) % n
end
```
Можем заметить, что мы увеличиваем хвост, но делаем это по модулю `n`, это сделано для того, чтобы не выходить за границу массива.

### Pop
```Pascal
function pop()
begin
    if (!empty()) then
        head := (head + 1) % n
end
```

### Size (сколько элементов в очереди)
```Pascal
integer size()
begin
  if head > tail then
    return n - head + tail;
  else
    return tail - head;
end
```
Условие здесь пишется в тех случаях, когда элементов добавлялось очень много и `tail` стала меньше `head`. Можно представить массив как окружность, на которой отмечены две точки и нам нужно найти расстояние между этими точками.

## Дек
***Дек (от англ. deque — double ended queue)*** — структура данных, представляющая из себя список элементов, в которой добавление новых элементов и удаление существующих производится с обоих концов. Эта структура поддерживает как FIFO, так и LIFO, поэтому на ней можно реализовать как стек, так и очередь. В первом случае нужно использовать только методы головы или хвоста, во втором — методы push и pop двух разных концов. Дек можно воспринимать как двустороннюю очередь. 

![Дек](https://neerc.ifmo.ru/wiki/images/thumb/7/73/Deque1.png/200px-Deque1.png)

Он имеет следующие операции:
1. `empty` — проверка на наличие элементов,
2. `pushBack` (запись в конец) — операция вставки нового элемента в конец,
3. `popBack` (снятие с конца) — операция удаления конечного элемента,
4. `pushFront` (запись в начало) — операция вставки нового элемента в начало,
5. `popFront` (снятие с начала) — операция удаления начального элемента.

Простейшая реализация пишется с помощью двух указателей аналогично очереди. Код остаётся в качестве упражнения читателю.

## Связные списки
Связный список — базовая динамическая структура данных в информатике, состоящая из узлов, каждый из которых содержит как собственно данные, так и одну или две ссылки («связки») на следующий и/или предыдущий узел списка.

![Списки](https://evileg.com/media/users/Lila25mila/photos/photo_XfCgfjC.jpg)

Для обращения к элементам в списке нам нужен какой-нибудь ID. И у массивов этот ID есть - это просто индекс элемента в массиве. Тогда для создания элемента в списке мы будем использовать несколько массивов - пусть у нас будет массив `val`, в котором указано значение элемента списка, массив `next`, указывающий на ID (индекс в массиве) следующего элемента в списке, и, по желанию, массив `prev`, указывающий на элемент, предшествующий текущему.
Благодаря такой структуре мы можем без проблем добавлять и удалять элементы из нашего списка, достаточно хранить индекс первого элемента в списке (назовём, допустим, "head"), а дальше мы будем просто перепривязывать элементы.
### Add
```Pascal
function addnew(x, i: integer) // Вставляет элемент на i-тое место (до него будет i элементов)
begin
    cnt := cnt + 1;
    val[cnt] = x
    integer ind := head;
    for j := 1 to i - 1 do
    begin
        ind := next[ind];
    end
    if (i == 0) then
        next[cnt] = head
        head = cnt
    else
        begin
            k := next[ind] //k - вспомогательная переменная
            next[ind] := cnt;
            next[cnt] := k;
        end
end 
```
### Delete
```Pascal
function del(x, i: integer) //Удаляет i-тый элемент в 0-индексации
begin
    int ind := head, p := -1;
    for i := 1 to i
        p := ind
        ind = next[ind];
    if (i == 0) then
        head = next[head];
    else
        next[p] = next[ind];
end
```

Это лишь один из возможных примеров реализации списка. Экспериментируйте и не стесняйтесь реализовывать списки по своему.

А нужны списки для реализации такой вещи как мультистек.

## Мультистек
Мультистек - это просто несколько стеков вместе. Допустим нам нужно 10000 стеков, каждый из которых должен держать в себе 100000 элементов. Если мы сделаем матрицу размером 10000 * 100000, то наш компьютер немножко умрёт. Именно поэтому здесь нам и пригодятся списки. Единственное отличие мультистека от обычного связного списка - это массив `last`, который указывает на индекс последнего элемента добавленного в i-тый стек.

### Push
```Pascal
function push(k, x: integer) // Добавляет X в стек с номером K
begin
    cnt := cnt + 1;
    val[cnt] := x;
    next[cnt] := last[k];
    last[k] := cnt;
end
```

### Pop
```Pascal
function pop(k: integer)
begin
    last[k] = next[last[k]];
end
```

### Top
```Pascal
integer top(k: integer)
begin
    return val[last[k]];
end
```

# Другие применения стека
*СКОРО!*