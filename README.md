# Understanding_JVM

## Код для исследования
```java

public class JvmComprehension {

    public static void main(String[] args) {
        int i = 1;                      // 1
        Object o = new Object();        // 2
        Integer ii = 2;                 // 3
        printAll(o, i, ii);             // 4
        System.out.println("finished"); // 7
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5
        System.out.println(o.toString() + i + ii);  // 6
    }
}

```
#### Сначала в JVM запускается ClassLoader. Идёт загрузка, проверка классов и инициализация статических элементов в Metaspace, которая находиться в RuntimeDataArea. Затем в StackMemory создаётся frame метода main()
1. Примитивная переменная i записывается во frame метода main?

2. Object создаётся в Heap, а его ссылка записывается в переменную "o".

3. Integer - это объектная обёртка примитивного типа int, создаётся в Heap и ссылка записывается в переменную.

4. В StackMemory создается следующий frame метода printAll() с параметрами.

5. Примитивный тип оборачикается в объект и кладётся в Heap, ссылка записывается в переменную "uselessVar".

6. В StackMemory создается следующий frame метода println() с параметрам. В параметрах оператор конкатинации парсит данные в строку, создается объект String и ссылка передается в параметрах. Затем метод исполняет свою функцию и frame удаляется. GarbageCollection удаляет неиспользуемые объекты.

7. В StackMemory создается следующий frame метода println() с параметрам. Создается объект String и ссылка передается в параметрах. Затем метод исполняет свою функцию и frame удаляется. GarbageCollection удаляет неиспользуемые объекты.

После, оставшиеся фреймы удаляются по принципу LI-FO.
