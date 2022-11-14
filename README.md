# lessons 5
# ООП

ООП ( Объе́ктно-ориенти́рованное программи́рование ) - методология программирования, основанная на представлении программы в виде совокупности объектов, каждый из которых является экземпляром определённого класса, а классы образуют иерархию наследования.

Классы в программировании состоят из свойств и методов. Свойства — это любые данные, которыми можно характеризовать объект класса. В нашем случае, объектом класса является студент, а его свойствами — имя, фамилия, оценки и средний балл.

У каждого студента есть имя — name и фамилия last_name . Также, у него есть промежуточные оценки за весь семестр. Эти оценки мы будем записывать в целочисленный массив из пяти элементов. После того, как все пять оценок будут проставлены, определим средний балл успеваемости студента за весь семестр — свойство average_ball.

Методы — это функции, которые могут выполнять какие-либо действия над данными (свойствами) класса. Добавим в наш класс функцию calculate_average_ball(), которая будет определять средний балл успеваемости ученика.

    1. Методы класса — это его функции.
    2. Свойства класса — его переменные ( Поле (атрибут) ).
    3. Интерфейс – это набор полей и методов класса, доступных для использования другими классами.
    4. Объект (экземпляр класса) – это отдельный представитель класса, имеющий конкретное
состояние и поведение, полностью определяемое классом.


Класс Студент ( для примера как не надо делать! )
```C++
class Students {
    private:
        // Итоговая оценка за семестр
        float average_ball;
    public:
        // Функция, считающая средний балл
        void calculate_average_ball()
        {
            int sum = 0; // Сумма всех оценок
            for (int i = 0; i < 5; ++i) {
                sum += scores[i];
            }
            // считаем среднее арифметическое
            average_ball = sum / 5.0;
        }

        // Имя студента
        std::string name;
        // Фамилия
        std::string last_name;
        // Пять промежуточных оценок студента
        int scores[5];
};
```

Четыре основных концепта ( принципа ) ООП:
  
  1. Абстрагирование – это способ выделить набор значимых характеристик объекта, исключая из
рассмотрения незначимые. Соответственно, абстракция – это набор всех таких характеристик.
  2. Инкапсуляция – это свойство системы, позволяющее объединить данные и методы, работающие
с ними, в классе и скрыть детали реализации от пользователя.
  3. Наследование – это свойство системы, позволяющее описать новый класс на основе уже
существующего с частично или полностью заимствующейся функциональностью. Класс, от
которого производится наследование, называется базовым или родительским. Новый класс –
потомком, наследником или производным классом.
  4. Полиморфизм – это свойство системы использовать объекты с одинаковым интерфейсом без
информации о типе и внутренней структуре объекта.

Синтаксис создания класса:
```C++
class <имя класса> : [<список базовых классов>]
{
  <список членов класса>
} [<список переменных>];
```
В классе есть три основных спецификатора доступа:

  1. private – закрытый член класса, доступ к такому члену класса имеют только члены-функции этого
же класса, а также дружественные функции, методы и классы;
  2. protected – защищённый член класса, доступ к такому члену класса имеют члены-функции этого
же класса, дружественные функции, методы и классы, а также члены-функции классов
наследников;
  3. public – открытый член класса, доступ к такому члену класса имеется всюду, где есть доступ к
самому классу; 

В ООП обычно переменные которые относятся к private секции именются с "_":
```C++
private:
  int _x;
  int _y;
```
!!!ВАЖНО!!! Если не указан спецификатор доступа тогда метод или поле класса автоматом явл-ся private.

**Плюсы инкапсуляции**

    1. Инкапсулированные классы проще в использовании и уменьшают сложность программ.
    2. Инкапсулированные классы помогают защитить данные и предотвращают их неправильное
использование. 
    3. Инкапсулированные классы проще поддерживать.
    4. Инкапсулированные классы проще отлаживать.

# Функции доступа и указатель this
В зависимости от класса, может потребоваться возможность получать/устанавливать значения
закрытым членам-данных класса. Функция доступа — это короткая открытая функция, задачей
которой является получение или изменение значения закрытой переменной-члена класса. В
зависимости от решаемых задач их разделяют на сеттеры и геттеры.

**геттеры** — это функции, которые возвращают значения закрытых переменных-членов класса;
**сеттеры** — это функции, которые позволяют присваивать значения закрытым переменным-
членам класса.

Например:
```C++
class MyString {
private:
  char *_string; // динамически выделяемая строка
  int _length; // переменную для хранения длины строки
public:
  int getLength() { return length; } // функция доступа для получения значения длины строки
  void setLength(const int& value = 0) { length = value; }
  //...
};
```

При компиляции методов, компилятор неявно добавляет к нему параметр *this. Указатель 
*this — это скрытый константный указатель, содержащий адрес объекта, который вызывает
метод класса. Как правило его используют если есть необходимость разрешить конфликт имен.
например если параметр метода и член класса к которому обращаются в теле этого метода имеют
одинаковые имена, то в этом случае. для явной адресации члена класса используют запись.

```C++
class DateClass
{
private:
  unsigned day;
  unsigned month;
  unsigned year;
public:
  void SetDate(unsigned day, unsigned month, unsigned year) {
    if(day > 0 && day <= 31) this->day = day;
    if(month > 0 && month <= 12) this->month = month;
    if(year <= 9999) this->year = year;
  }
  void Print() {
    printf("%02u.%02u.%04u", day, month, year);
  }
};
```

# Конструкторы и Деструкторы
**Конструктор** — это особый тип метода класса, который автоматически вызывается при создании
объекта этого класса. Конструкторы обычно используются для инициализации переменных-
членов класса значениями, которые предоставлены по умолчанию или пользователем, или для
выполнения некоторых предварительных действий необходимых для работы экземпляров
данного класса (например, открыть определенный файл, установить соединение с базой данных и
т.д.).

В отличие от обычных методов, конструкторы имеют определенные правила их именования:
    1.конструкторы всегда должны иметь то же имя, что и класс;
    2.конструкторы не имеют типа возврата (даже void).
    
Конструктор, который не имеет параметров (или содержит параметры, которые все имеют
значения по умолчанию), называется **конструктором по умолчанию**.

```C++
class Data{
private:
  int _data;
public:
  Data(){
    _data = 10;
  }
```

Параметрический конструктор - такой же конструктор, но уже с параметрами ( они могут быть и по умолчанию ).
```C++
class Data{
private:
  int _data;
public:
  Data(int value = 10){
    _data = value;
  }
```
! В данном примере _data = value; и значение value по умолчанию 10 ( _data будет равно 10 если value не будет задано пользователем ) !

**Деструктор** — это специальный тип метода класса, который выполняется при удалении объекта
класса. В то время как конструкторы предназначены для инициализации класса, деструкторы
предназначены для очистки памяти после него.

Так же, как и конструкторы, деструкторы имеют свои особенности именования:

    1. деструктор должен иметь то же имя, что и класс, со знаком тильда (~) в самом начале;
    2. деструктор не может принимать аргументы;
    3. деструктор не имеет возвращаемого значени;
    
Cинтаксис создания деструктора:
```C++
~<имя класса>()
```
```C++
class Array
{
private:
double* data;
unsigned size;
public:
  Array(unsigned size = 0) {
    std::cout << "Create\n";
    data = new double[size];
    this->size = size;
  }
  ~Array() {
    std::cout << "Destroy\n"; // обычно в деструкторе не выводят никаких сообщений на экран ( консоль )
    delete []data;
  }
  double& Element(unsigned i) {
    return data[i];
  }
  unsigned GetSize(){return size;}
};
void ArrayWork(){
  Array a(5);
  for (int i = 0; i < a.GetSize(); i++) {
    a.Element(i) = i*i;
  }
  for (int i = 0; i < a.GetSize(); i++) {
    std::cout << "%lf ", a.Element(i);
  }
  std::endl;
  }
int main() {
  ArrayWork();
  getchar();
}
```

# Конструктор копирования
Конструктор копирования инициализирует объект, копируя значения элементов из объекта того же типа.
Синтаксис:
```C++
<имя класса>(const <имя класса> &<имя параметра>)
```
Например:
```C++
public:
  // конструктор копирования
  Array(const Array& a) {
    std::cout << "Copy\n";
    data = new double[a.size];
    size = a.size;
    for (int i = 0; i < a.size; i++) data[i] = a.data[i];
  }
```

# Список Инициализации
В примерах ранее мы инициализировали члены класса в конструкторе, используя оператор
присваивания. При таком подходе сначала создаются члены-данные, а затем выполняется тело
конструктора, где этим переменным присваиваются значения. Однако некоторые типы данных
(например, константы и ссылки) должны быть инициализированы сразу. Так, например, такой код
не будет скомпилирован:
```C++
class Value {
private:
  const int value;
public:
  // Value::value: требуется инициализация в списке инициализации базовых классов и членов
  Value() {
    value = 3; // левостороннее значение указывает на объект-константу (const)
  }
};
```

Ошибка компиляции происходит, поскольку приведенный код аналогичен следующему коду (без
привязки к ООП):
```C++
const int value; // объект const необходимо инициализировать, если он не внешний
value = 3; // value: невозможно присваивать значения переменной, которая объявлена
как константа
```
Для решения этой проблемы в C++ добавили возможность инициализации членов-данных класса
через список инициализации после объявления конструктора, вместо присваивания им значений
после объявления. Синтаксис списка инициализации следующий:
```C++
<имя конструктора>(<список параметров>):<список инициализации>
```
Сам список инициализации представляет собой конструкцию вида:
```C++
<имя поля>(<значение>),...
```
Таким образом поставленную выше проблему можно решить следующим образом:
```C++
class Value {
private:
  const int value;
public:
  Value(): value(3)
  {
  }
};
```

# Применение ключевого слова default. Общая форма
Ключевое слово default введено в C++ 11. Его использование указывает компилятору самостоятельно генерировать (использовать) соответствующую функцию класса, если таковая не объявлена в классе.

Как известно, компилятор автоматически генерирует ряд конструкторов класса и деструктор. Указание ключевого слова default для этих функций дает следующие взаимосвязанные преимущества:

        1. программист получает понятную информацию об отсутствии реализации отдельных функций в классе. Используються компиляторные версии этих функций;
        2. упрощается восприятие информации об особенностях использования тех или иных функций класса. Вместо того чтобы вспоминать правила программист                  указывает то, что хочет получить.
        
Общая форма использования ключевого слова default для конструкторов класса следующая:
```C++
class ClassName {
    // ...

    ClassName(parameters) = default;

    // ...
};
```
где

    1. ClassName – имя класса, в котором использовано ключевое слово default;
    2. ClassName(parameters) – один из конструкторов класса, которые автоматически генерируются компилятором;
    3. parameters – список параметров, который принимает специальная функция класса, которая генерируется автоматически. Список параметров может                    отсутствовать (конструктор по умолчанию).
    
Общая форма использования ключевого слова default для деструктора класса:
```C++
class ClassName {
    // ...

    ~ClassName() = default;

    // ...
};
```

Полезная ссылочка:
https://ru.wikipedia.org/wiki/%D0%9F%D1%80%D0%B0%D0%B2%D0%B8%D0%BB%D0%BE_%D1%82%D1%80%D1%91%D1%85_(C%2B%2B)#%D0%9F%D1%80%D0%B0%D0%B2%D0%B8%D0%BB%D0%BE_%D0%BF%D1%8F%D1%82%D0%B8
