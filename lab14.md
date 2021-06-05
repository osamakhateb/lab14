# Отчет по лабораторной работе №14

----

### Средства, применяемые при разработке программного обеспечения в ОС типа UNIX/Linux

----

## Российский Университет Дружбы Народов

### Факультет Физико-Математических и Естественных Наук

*Дисциплина: Операционные системы*

Студент: Алхатиб Осама

Группа: НПИбд-02-20

2021г.

---

1. ***Цель работы***

Приобрести простейшие навыки разработки, анализа, тестирования и отладки
приложений в ОС типа UNIX/Linux на примере создания на языке программирования С калькулятора с простейшими функциями

---

2 Задание
1. В домашнем каталоге создайте подкаталог ~/work/os/lab_prog.
2. Создайте в нём файлы: calculate.h, calculate.c, main.c. Это будет примитивнейший калькулятор, способный складывать, вычитать, умножать
и делить, возводить число в степень, брать квадратный корень, вычислять sin, cos, tan. При запуске он будет запрашивать первое число,
операцию, второе число. После этого программа выведет результат и
остановится. Реализация функций калькулятора в файле calculate.h:
//////////////////////////////////// // calculate.c #include <stdio.h> #include
<math.h> #include <string.h> #include “calculate.h” float Calculate(float
Numeral, char Operation[4]) { float SecondNumeral; if(strncmp(Operation,
“+”, 1) == 0) { printf(“Второе слагаемое:”); scanf(“%f”,&SecondNumeral);
return(Numeral + SecondNumeral); } else if(strncmp(Operation, “-”, 1) ==
0) { printf(“Вычитаемое:”); scanf(“%f”,&SecondNumeral); return(Numeral
- SecondNumeral); } else if(strncmp(Operation, “”, 1) == 0) { printf(”Множитель: ”); scanf(”%f”,&SecondNumeral); return(Numeral SecondNumeral); } else
if(strncmp(Operation,”/“, 1) == 0) { printf(”Делитель: “); scanf(”%f“,&SecondNumeral);
if(SecondNumeral == 0) { printf(”Ошибка: деление на ноль! “); return(HUGE_VAL);
} else return(Numeral / SecondNumeral); } else if(strncmp(Operation,”pow“, 3)
== 0) { printf(”Степень: “); scanf(”%f“,&SecondNumeral); return(pow(Numeral,
SecondNumeral)); } else if(strncmp(Operation,”sqrt“, 4) == 0) return(sqrt(Numeral));
else if(strncmp(Operation,”sin“, 3) == 0) return(sin(Numeral)); else
if(strncmp(Operation,”cos“, 3) == 0) return(cos(Numeral)); else if(strncmp(Operation,”tan“,
3) == 0) return(tan(Numeral)); else { printf(”Неправильно введено действие
”); return(HUGE_VAL); } } Интерфейсный файл calculate.h, описывающий
формат вызова функциикалькулятора: /////////////////////////////////////// //
calculate.h #ifndef CALCULATE_H_ #define CALCULATE_H_ float Calculate(float
Numeral, char Operation[4]); #endif /CALCULATE_H_/ Основной файл main.c,
реализующий интерфейс пользователя к калькулятору: ////////////////////////////////////////
// main.c
3. Выполните компиляцию программы посредством gcc: gcc -c calculate.c gcc
-c main.c gcc calculate.o main.o -o calcul -lm
4. При необходимости исправьте синтаксические ошибки.
5. Создайте Makefile со следующим содержанием:
# # Makefile # CC = gcc CFLAGS = LIBS = -lm calcul: calculate.o main.o gcc
calculate.o main.o -o calcul $(LIBS) calculate.o: calculate.c calculate.h gcc -c
calculate.c $(CFLAGS) main.o: main.c calculate.h gcc -c main.c $(CFLAGS) clean: -rm
calcul .o ~ # End Makefile Поясните в отчёте его содержание.
6. С помощью gdb выполните отладку программы calcul (перед использованием gdb исправьте Makefile): – Запустите отладчик GDB, загрузив в него
программу для отладки: gdb ./calcul – Для запуска программы внутри отладчика введите команду run: run – Для постраничного (по 9 строк) просмотра
исходного код используйте команду list: list – Для просмотра строк с 12 по
15 основного файла используйте list с параметрами: list 12,15 – Для просмотра определённых строк не основного файла используйте list с параметрами: list calculate.c:20,29 – Установите точку останова в файле calculate.c на
строке номер 21: list calculate.c:20,27 break 21 – Выведите информацию об
имеющихся в проекте точка останова: info breakpoints – Запустите программу внутри отладчика и убедитесь, что программа остановится в момент
прохождения точки останова: run 5
• backtrace – Отладчик выдаст следующую информацию: #0 Calculate
(Numeral=5, Operation=0x7fffffffd280 “-”) at calculate.c:21 #1 0x0000000000400b2b
in main () at main.c:17 а команда backtrace покажет весь стек вызываемых
функций от начала программы до текущего места. – Посмотрите, чему
равно на этом этапе значение переменной Numeral, введя: print Numeral
На экран должно быть выведено число 5. – Сравните с результатом вывода
на экран после использования команды: display Numeral – Уберите точки
останова: info breakpoints delete 1
7. С помощью утилиты splint попробуйте проанализировать коды файлов
calculate.c и main.c

---

***1. Выполнение лабораторной работы***
1. В домашнем каталоге создал подкаталог ~/work/os/lab_prog.
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/1.png)

**Figure 3.1: каталог**
2. Создал в нём файлы: calculate.h, calculate.c, main.c.
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/2.png)

**Figure 3.2: файлы:**
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/3.png)

**Figure 3.3: calculate.h файл**
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/5.png)
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/6.png)
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/7.png)
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/4.png)

**Figure 3.4: calculate.c файл**
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/8.png)
 
 **Figure 3.5: main.c файл**
3. Выполнил компиляцию программы посредством gcc
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/9.png)
Figure 3.6: компиляция gcc
4. Исправил синтаксические ошибки в файле main.c (удалил & перед operator
в линии scanf(“%s”,&Operation);)
5. Создал Makefile со следующим содержанием
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/10.png)


**Figure 3.7: Makefile**
1. С помощью gdb выполнил отладку программы calcul (перед использованием
gdb исправьте Makefile)
• Запустил отладчик GDB, загружил в него программу для отладки: gdb ./calcul
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/11.png)

**Figure 3.8: gdb**
• Для запуска программы внутри отладчика ввел команду run: run
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/12.png)

**Figure 3.9: run**
• Для постраничного (по 9 строк) просмотра исходного код использовал команду list: list
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/13.png)

**Figure 3.10: list**
• Для просмотра строк с 12 по 15 основного файла использовал list с параметрами: list 12,15
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/14.png)

**Figure 3.11: list**
• Для просмотра определённых строк не основного файла использовал list с
параметрами: list calculate.c:20,29
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/15.png)

**Figure 3.12: list**
• Установил точку останова в файле calculate.c на строке номер 21: list
calculate.c:20,27 break 21
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/16.png)

**Figure 3.13: list**
• Вывел информацию об имеющихся в проекте точка останова: info
breakpoints
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/17.png)

**Figure 3.14: breakpoints**
• Запустил программу внутри отладчика и убедитесь, что программа остановится в момент прохождения точки останова: run 5
• backtrace
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/18.png)

**Figure 3.15: run**
• Посмотрил, чему равно на этом этапе значение переменной Numeral, введя:
print Numeral
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/19.png)

**Figure 3.16: print**
• Сравнил с результатом вывода на экран после использования команды:
display Numeral
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/20.png)

**Figure 3.17: display**
• Убрал точки останова: info breakpoints delete 1
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/21.png)

**Figure 3.18: delete**
7. С помощью утилиты splint попробовал проанализировать коды файлов
calculate.c и main.c.
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/22.png)

**Figure 3.19: splint calculate.c**
![](https://raw.githubusercontent.com/osamakhateb/lab14/main/image/23.png)
**Figure 3.20: splint main.c**

---

4. Выводы
В результате работы , я приобрёл простейшие навыки разработки, анализа, тестирования и отладки приложений в Линук

---

5 Контрольные вопросы
1. Дополнительную информацию о этих программах можно получить с помощью функций info и man.
2. Unix поддерживает следующие основные этапы разработки приложений:
-создание исходного кода программы;
• представляется в виде файла;
-сохранение различных вариантов исходного текста;
-анализ исходного текста; Необходимо отслеживать изменения исходного кода,
а также при работе более двух программистов над проектом программы нужно,
чтобы они не делали изменений кода в одно время.
-компиляция исходного текста и построение исполняемого модуля;
-тестирование и отладка;
-проверка кода на наличие ошибок
-сохранение всех изменений, выполняемых при тестировании и отладке.
3. Использование суффикса “.с” для имени файла с программой на языке Си
отражает удобное и полезное соглашение, принятое в ОС UNIX. Для любого
имени входного файла суффикс определяет какая компиляция требуется.
Суффиксы и префиксы указывают тип объекта. Одно из полезных свойств
компилятора Си — его способность по суффиксам определять типы файлов.
По суффиксу .c компилятор распознает, что файл abcd.c должен компилироваться, а по суффиксу .o, что файл abcd.о является объектным модулем и для получения исполняемой программы необходимо выполнить редактирование связей. Простейший пример командной строки для компиляции
программы abcd.c и построения исполняемого модуля abcd имеет вид: gcc
-o abcd abcd.c. Некоторые проекты предпочитают показывать префиксы
в начале текста изменений для старых (old) и новых (new) файлов. Опция
– prefix может быть использована для установки такого префикса. Плюс к
этому команда bzr diff -p1 выводит префиксы в форме которая подходит
для команды patch -p1.
4. Основное назначение компилятора с языка Си заключается в компиляции
всей программы в целом и получении исполняемого модуля.
5. При разработке большой программы, состоящей из нескольких исходных
файлов заголовков, приходится постоянно следить за файлами, которые
требуют перекомпиляции после внесения изменений. Программа make
освобождает пользователя от такой рутинной работы и служит для документирования взаимосвязей между файлами. Описание взаимосвязей и
соответствующих действий хранится в так называемом make-файле, который по умолчанию имеет имя makefile или Makefile.
6. makefile для программы abcd.c мог бы иметь вид:
9. 1) Выполнили компиляцию программы 2)Увидели ошибки в программе
7) Открыли редактор и исправили программу 4) Загрузили программу в отладчик gdb 5) run — отладчик выполнил программу, мы ввели
требуемые значения. 6) программа завершена, gdb не видит ошибок.
10. 1 и 2.) Мы действительно забыли закрыть комментарии; 3.) отладчику не
понравился формат %s для &Operation, т.к %s — символьный формат, а
значит необходим только Operation.
11. Если вы работаете с исходным кодом, который не вами разрабатывался,
то назначение различных конструкций может быть не совсем понятным.
Система разработки приложений UNIX предоставляет различные средства,
повышающие понимание исходного кода. К ним относятся:
– cscope - исследование функций, содержащихся в программе;
– splint — критическая проверка программ, написанных на языке Си.
12. 1. Проверка корректности задания аргументов всех исп
функций, а также типов возвращаемых ими значений;
2. Поиск фрагментов исходного текста, корректных с точки зрения синтаксиса языка Си, но малоэффективных с точки зрения их реализации или
содержащих в себе семантические ошибки;
3. Общая оценка мобильности пользовательской программы.
