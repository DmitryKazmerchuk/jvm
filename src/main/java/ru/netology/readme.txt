

public class JvmComprehension {              // 1. Подсистема загрузчиков классов ClassLoaders подгружает классы:
					                         //    Application ClassLoaders -> Platform ClassLoaders -> Bootstrap ClassLoaders
					                         //    (подгружает классы из стандартной библиотеки Java, в нашем случае
					                         //    String[] args) -> Platform ClassLoaders (подгружает зависимости, в нашем проекте их нет) ->
					                         //    -> Application ClassLoaders (загружает public class JvmComprehension);

					                         // 2. Подгружаем public class JvmComprehension и др. системные классы в Metaspase;

    public static void main(String[] args) { // 3. Создаём фрейм main() в Stack Memory;
        int i = 1;                           // 4. Создаём и инициализируем примитив int i = 1 в Stack Memory -> фрейм main();
        Object o = new Object();             // 5. Создаём объект в Heap и создаём ссылку на объект "o" в Stack Memory -> фрейм main();
        Integer ii = 2;                      // 6. Создаём объект в Heap и создаём ссылку на объект "ii" в Stack Memory -> фрейм main();
        printAll(o, i, ii);                  // 7. Создаём фрейм printAll() в Stack Memory -> создаём вторые ссылки на Object o, Integer ii
                                             //    и передаём значение переменной int i = 1;
        System.out.println("finished");      // 10. Передаём в фрейм System.out.println() -> "finished";
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 8. Создаём объект Integer uselessVar = 700 в Heap и создаём ссылку на объект
                                                    //    "uselessVar" в Stack Memory -> фрейм printAll();
						                            // 11. Сборщик мусора удаляет объект "uselessVar", так как на него никто не ссылается;
        System.out.println(o.toString() + i + ii);  // 9. Создаём фрейм toString() в Stack Memory -> передаём ссылку на объект "о",
                                                    //    создаём фрейм System.out.println() -> передаём ссылку на обект "o" в фрейме
                                                    //    toString(), передаём ссылку на объект ii, передаём значение переменной int i = 1;
    }
}