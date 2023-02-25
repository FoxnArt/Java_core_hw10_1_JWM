# Код для исследования

public class JvmComprehension {  
    //Сначала JVM запрашивает ClassLoader-ы загрузить класс JvmComprehension
    и базовые классы System, Integer в область Metaspace, затем подсистема загрузчиков
    классов проверяет подготавливает код и связывает ссылки

    public static void main(String[] args) { //В Stack Memory создается фрейм main() (см.рисунок ниже) 
        int i = 1;                      
        // В стеке создается переменная i со значением 1
        Object o = new Object();        
        // Оператор new выделаяет память в куче, конструктор создает объект, 
        // и ссылка на объект присваивается переменной o
        Integer ii = 2;
        // Создается обертка ссылочного типа в куче, и ссылка на объект присваивается переменной ii
        printAll(o, i, ii);
        // В Stack Memory создается фрейм printAll() и трасер переходит туда
        System.out.println("finished"); 
        // В стеке создается новый фрейм System.out.println() и туда передается значение "finished" 
    }

    private static void printAll(Object o, int i, Integer ii) { 
        // Создаются три переменные, две будут содержать ссылки на созданные ранее 
        // объекты Object и Integer, а одна примитивного типа со значением 1
        Integer uselessVar = 700;
        // Создается обертка ссылочного типа в куче, и ссылка на объект 
        // присваивается переменной uselessVar
        System.out.println(o.toString() + i + ii);
        // В стеке создается новый фрейм System.out.println() и туда передаются
        // ссылки на объекты о, ii, и примитив int i = 1
    }   // После завершения работы метода из стека выгружаются фреймы System.out.println() и printAll()

}  
// После завершения работы программы фреймы System.out.println() и main() выгружаются   
// из стека. А сборщик мусора удаляет недостижимые объекты из кучи.
![](/memory.jpg)