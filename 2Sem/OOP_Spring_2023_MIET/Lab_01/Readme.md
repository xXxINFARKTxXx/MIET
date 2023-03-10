[<назад>](https://github.com/xXxINFARKTxXx/MIET/tree/main/2Sem/OOP_Spring_2023_MIET)
# Лабораторная работа №1 (Вариант 1)
## Цель работы
Цель работы: Закрепить практические навыки, полученные при изучении дисциплины «Основы программирования».  Решение задач с использованием динамических структур, работа с файлами.

## Техническое задание

### Общие требования 
1. Во всех вариантах нужно создать базу данных, согласно варианту задания
2. В каждой базе должна быть статическая переменная для учета общего числа элементов в базе данных.
3. Данные размещаются в динамической памяти.
4. Обязательные функции для всех вариантов:
  • добавить новый элемент в базу
  • распечатка данных в табличном виде
  • выход из программы
5. Остальные функции для работы с базой указаны в задании индивидуально.
6. Для выполнения функций, указанных в задании, написать диалоговый интерфейс, позволяющий выполнять функции в произвольном порядке многократно
7. При выполнении функции «выход из программы» нужно сохранить базу на диске
8. Первичное создание базы – ввод данных с клавиатуры
9. Если программа уже запускалась, то данные загружаются из файла перед выходом на диалог. Иными словами вносятся изменения и дополнения в уже существующую базу данных.
10.  При реализации функций в параметрах и возвращаемых значениях использовать указатели и ссылки
    
    
### Требования по варианту
+ База данных: Пищевое производство (расчеты).
+ Создать класс food (видоизменить программу) со следующими элементами:

    ```c++
    char* fam ;	           //Название изделия
    int   type;	            //тип изделия (1- булочка, 2-пирожок, 3-пирожное)
    double weight;	// вес
    int quant;		// количество
    double cost;		//стоимость
    ```
+ Создать обязательные функции, указанные в общих требованиях.  
+ Создать функции для данного варианта:  
  • Поиск изделий по названию  
  • Фильтр по типу (найти изделия заданного типа)  
  • Сортировать по уменьшению стоимости (сначала более дорогие).  
+ Тестовая программа №1:  
    • Базу данных (массив объектов) располагать в динамической памяти.  
    • При запуске программы данные ввести с клавиатуры (первый запуск программы) или загрузить с диска (все последующие запуски).  
    • Добавить несколько новых элементов (ввод с клавиатуры).  
    • Выполнить все реализованные функции (поиск, фильтр, сортировка).  
    • При выходе из программы запомнить измененную базу на диске.  

### Пример диалогового интерфейса (База данных «Склад товаров»)
![image](https://user-images.githubusercontent.com/57076699/221278362-82021063-f4c1-428b-9342-7202cbf5acd8.png)

### Пример распечатки данных в табличном виде (База данных «Склад товаров»)
![image](https://user-images.githubusercontent.com/57076699/221285525-babe4c51-90ee-4f44-bf6c-b5434ff33de8.png)

## Реализация технического задания

### Сторонние возможности
При реализации программы были использованы следующие возможности из библиотек:
```c++
#include <fstream> // работа с файлами
#include <iostream> // работа с потоками ввода-вывода
#include <iomanip>  // и его модификация 
#include <string>                     // работа со строками
#include <boost/algorithm/string.hpp> // работа со строками
#include <cmath> // сравнение вещественных чисел
```

### Пример работы программы

##### Начало работы (меню программы)
```
--------------------------------------------------------------------------------------------------------------------------------------
Add new product..................1
Print product database...........2
Find product by name.............3
Filter database by price.........4
Sort database by lowering price..5
Filter database by product type..6
Exit program.....................7

Enter option: 
```
> На любой невалидный ввод программа регирует следующим образом: ``` Wrong input!```.
> Кроме того программа прекращает взаимодействовать с пользователем в районе данной опции программы и выводит меню.
> Например:
```
Enter option: 4
Enter product price and press Enter: ;;;;;;;;;;
Wrong input!

...
\\\ Menu
...
```

##### Добавление элемента в базу и вывод базы на экран
```
...
Enter option: 1
Enter product name (all symbols except ';') and press Enter: Name  
Enter product type(1 - bun, 2 - pie, 3 - cake) and press Enter: 1
Enter product price and press Enter: 123
Enter product weight and press Enter: 321
Enter product quantity and press Enter: 100
Item added!

...
/// Menu
...

Enter option: 2

Name of product                         Type      Weight              Quantity            Price(rub)          Total Price         
--------------------------------------------------------------------------------------------------------------------------------------
cake12                                  cake      0.2                 5                   500                 2500                
pie3                                    pie       3.14                15                  199                 2985                
cake2                                   cake      0.8                 13                  175                 2275                
cake3                                   cake      5.9                 4                   145                 580                 
bun3                                    bun       2.78                47                  123                 5781                
bun10                                   bun       0.4                 21                  65                  1365                
bun2                                    bun       0.6                 92                  25                  2300                
pie2                                    pie       1.3                 41                  20                  820                 
pie35                                   pie       0.3                 14                  15                  210                 
2                                       cake      5                   6                   4                   24                  
qwe                                     bun       1                   1                   1                   1                   
Name                                    bun       321                 100                 123                 12300               
--------------------------------------------------------------------------------------------------------------------------------------
Total price of all products:..................................................................................31141
Total positions:..............................................................................................12

...
/// Menu
...

Enter option:
```


##### Поиск продукта по имени
```
...
Enter option: 3
Enter product name (all symbols except ';') and press Enter: Name

Name of product                         Type      Weight              Quantity            Price(rub)          Total Price         
--------------------------------------------------------------------------------------------------------------------------------------
Name                                    bun       321                 100                 123                 12300               
--------------------------------------------------------------------------------------------------------------------------------------
Total price of all products:..................................................................................12300
Total positions:..............................................................................................1

... 
\\\ Menu
...

Enter option: 

```

##### Вывести по фильтру "Цена"
```
...
Enter option: 4
Enter product price and press Enter: 75
Enter filter type:
0 - less than chosen price
1 - more than chosen price
2 - equal to chosen price
and press Enter: 1

Name of product                         Type      Weight              Quantity            Price(rub)          Total Price         
--------------------------------------------------------------------------------------------------------------------------------------
cake12                                  cake      0.2                 5                   500                 2500                
pie3                                    pie       3.14                15                  199                 2985                
cake2                                   cake      0.8                 13                  175                 2275                
cake3                                   cake      5.9                 4                   145                 580                 
bun3                                    bun       2.78                47                  123                 5781                
Name                                    bun       321                 100                 123                 12300               
--------------------------------------------------------------------------------------------------------------------------------------
Total price of all products:..................................................................................1265
Total positions:..............................................................................................6
...
```

##### Сортировка
```
...
Enter option: 5
Base sorted!

...
/// Menu
...

Enter option: 2

Name of product                         Type      Weight              Quantity            Price(rub)          Total Price         
--------------------------------------------------------------------------------------------------------------------------------------
cake12                                  cake      0.2                 5                   500                 2500                
pie3                                    pie       3.14                15                  199                 2985                
cake2                                   cake      0.8                 13                  175                 2275                
cake3                                   cake      5.9                 4                   145                 580                 
Name                                    bun       321                 100                 123                 12300               
bun3                                    bun       2.78                47                  123                 5781                
bun10                                   bun       0.4                 21                  65                  1365                
bun2                                    bun       0.6                 92                  25                  2300                
pie2                                    pie       1.3                 41                  20                  820                 
pie35                                   pie       0.3                 14                  15                  210                 
2                                       cake      5                   6                   4                   24                  
qwe                                     bun       1                   1                   1                   1                   
--------------------------------------------------------------------------------------------------------------------------------------
Total price of all products:..................................................................................31141
Total positions:..............................................................................................12

...
```

##### Отфильтровать по типу продукта
```
...
Enter option: 6
Enter product type(1 - bun, 2 - pie, 3 - cake) and press Enter: 2

Name of product                         Type      Weight              Quantity            Price(rub)          Total Price         
--------------------------------------------------------------------------------------------------------------------------------------
pie3                                    pie       3.14                15                  199                 2985                
pie2                                    pie       1.3                 41                  20                  820                 
pie35                                   pie       0.3                 14                  15                  210                 
--------------------------------------------------------------------------------------------------------------------------------------
Total price of all products:..................................................................................234
Total positions:..............................................................................................3

...
```

##### Выход и сохранение
```
...
Enter option: 7
Do you want to save changes? Press 'ENTER' to save, any other key to cancel changes.
Changes saved!
>> exit
...
```

### Листинг исходного кода:
- [main.cpp](https://github.com/xXxINFARKTxXx/OOP2023SpringMIET/edit/main/Lab_01/main.cpp)  
- [utility.h](https://github.com/xXxINFARKTxXx/OOP2023SpringMIET/edit/main/Lab_01/utility.h)  
- [base.cpp](https://github.com/xXxINFARKTxXx/OOP2023SpringMIET/edit/main/Lab_01/base.cpp)  
- [base.h](https://github.com/xXxINFARKTxXx/OOP2023SpringMIET/edit/main/Lab_01/base.h)  


[<назад>](https://github.com/xXxINFARKTxXx/MIET/tree/main/2Sem/OOP_Spring_2023_MIET)
