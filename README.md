# Курсовой проект по курсу Java-разработчик "Менеджер задач"

### Задачи:
разработать сервер, отвечающий за менеджмент списка дел. Разработать нужно на базе заготовки, разработать unit-тесты для класса Todos и реализовать его бизнес логику.

### Используемые технологии Java, Stream API, Maven, библиотеки: Gson, TDD: Junit 5, Hamcrest;

## Результат: 
- Разработаны unit-тесты на основные методы класса [Todos](https://github.com/Omen1984/coursework-nethology-task-manager/blob/master/src/test/java/ru/netology/javacore/TodosTests.java) с применением библиотеки Hamcrest, так как тесты написаны с использованием этой библиотеки становятся более лаконичными и понятными
#### Пример теста:
```java
 @Test
    public void testTodos_getAllTasks() {
        String task1 = "Пробежка";
        String task2 = "Акробатика";
        String task3 = "Учёба";
        String expected = "Акробатика Пробежка Учёба";

        sut.addTask(task1);
        sut.addTask(task2);
        sut.addTask(task3);
        String result = sut.getAllTasks();

        assertThat(result, equalTo(expected));
    }
```

- Была реализована бизнес логика класса Todos - его методы добавления, удаления и показа всех задач

```java
public class Todos {
    private List<String> todos;

    public Todos() {
        todos = new ArrayList<>();
    }

    public void addTask(String task) {
        todos.add(task);
    }

    public void removeTask(String task) {
        todos.remove(task);
    }

    public String getAllTasks() {
        return todos.stream()
                .sorted(Comparator.naturalOrder())
                .collect(Collectors.joining(" "));
    }

}
```

- Написан простой сервер в классе Main с помощью класса ServerSocket, который принимает строку от клиента в формате JSON, Пример строки:
```json
{
    "type": "ADD", 
    "task": "Прогулка с собакой" 
}
```
