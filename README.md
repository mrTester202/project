# lessons 8
# Перегрузка операций C++
Перегрузка операторов позволяет определить действия, которые будет выполнять оператор. Перегрузка подразумевает создание функции, название которой содержит слово operator и символ перегружаемого оператора. Функция оператора может быть определена как член класса, либо вне класса.

Перегрузить можно только те операторы, которые уже определены в C++. Создать новые операторы нельзя.

Если функция оператора определена как отдельная функция и не является членом класса, то количество параметров такой функции совпадает с количеством операндов оператора. Например, у функции, которая представляет унарный оператор, будет один параметр, а у функции, которая представляет бинарный оператор, - два параметра. Если оператор принимает два операнда, то первый операнд передается первому параметру функции, а второй операнд - второму параметру. При этом как минимум один из параметров должен представлять тип класса.

Пример:
```C++
#include <iostream>
 
class Counter {
public:
    Counter(int sec) {
        seconds = sec;
    }
    void display() {
        std::cout << seconds << " seconds" << std::endl;
    }
int seconds;
};
 
Counter operator + (Counter c1, Counter c2) {
    return Counter(c1.seconds + c2.seconds);
}
```
Здесь функция оператора не является частью класса Counter и определена вне его. Данная функция перегружает оператор сложения для типа Counter. Она является бинарной, поэтому принимает два параметра. В данном случае мы складываем два объекта Counter. Возвращает функция также объект Counter, который хранит общее количесто секунд. То есть по сути здесь операция сложения сводится к сложению секунд обоих объектов:

Операторы сравнения:
```C++
bool operator == (Counter c1, Counter c2) {
    return c1.seconds == c2.seconds;
}
bool operator != (Counter c1, Counter c2) {
    return c1.seconds != c2.seconds;
}
bool operator > (Counter c1, Counter c2) {
    return c1.seconds > c2.seconds;
}
bool operator < (Counter c1, Counter c2) {
    return c1.seconds < c2.seconds;
}
int main() {
    Counter c1(20);
    Counter c2(10);
    bool b1 = c1 == c2;     // false
    bool b2 = c1 > c2;       // true
 
    std::cout << b1 << std::endl;
    std::cout << b2 << std::endl;
     
    return 0;
}
```
Оператор присваивания:
```C++
Counter& operator += (Counter c2) {
  seconds += c2.seconds; 
  return *this;
}
```

Операторы Инкремент и Декремент:
```C++
// префиксные операторы
Counter& operator++ () {
    seconds += 5;
    return *this;
}
Counter& operator-- () {
    seconds -= 5;
    return *this;
}
// постфиксные операторы
Counter operator++ (int) {
    Counter prev = *this;
    ++*this;
    return prev;
}
Counter operator-- (int) {
    Counter prev = *this;
    --*this;
    return prev;
}
```
