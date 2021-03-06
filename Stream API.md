# Stream API

### Чем Stream отличается от коллекции?
Интерфейс` java.util.stream.Stream<T>` — поток объектов для преобразования коллекций, массивов. В потоке не хранятся элементы операции, он не модифицирует источник, а формирует в ответ на действие новый поток. Операции в потоке не выполняются до момента, пока не потребуется получить конечный результат выполнения. **Stream** нельзя воспринимать как просто поток ввода/вывода. Этот поток создается на основе коллекции/массива, элементы которой переходят в состояние информационного ожидания действия, переводящего поток в следующее состояние до достижения терминальной цели, после чего поток прекращает свое существование.

### Промежуточные и терминальные операции.
#### Промежуточные
- `filter(Predicate<? super T> predicate)` – выбор элементов из потока на основании работы предиката в новый поток. Отбрасываются все элементы, не удовлетворяющие условию предиката.
- `map(Function<? super T, ? extends R> mapper)` — изменение всех элементов потока, применяя к каждому элементу функцию mapper. Тип параметризации потока может изменяться, если типизация `T` и `R` относится к различным классам.
- `flatMap(Function<T, Stream<R>> mapper)` — преобразовывает один объект, как правило составной, в объект более простой структуры, например, массив в строку, список в объект, список списков в один список.
- `peek(Consumer<T> consumer)` — возвращает поток, содержащий все элементы исходного потока. Используется для просмотра элементов в текущем состоянии потока. Можно использовать для записи логов.
- `sorted(Comparator<T> comparator) и sort()` — сортировка в новый поток.
- `limit(long maxSize)` — ограничивает количество элементов выходящего потока заданным в параметре значением.
- `skip(long n)` — не включает в выходной поток первые n элементов исходного потока.
- `distinct()` — удаляет из потока все идентичные элементы.

#### Терминальные операции
Результатом может быть новая коллекция, объект некоторого класса, число. Промежуточные операции обязательно должны завершаться терминальными, иначе они не вы- полнятся, так как просто не имеют смысла.
- `void forEach(Consumer<T> action)` — выполняет действие над каждым элементом потока. Чтобы результат действия сохранялся, реализация action должна предусматривать фиксацию результата в каком-либо объекте или потоке вывода.
- `Optional<T> findFirst()` — находит первый элемент в потоке.
- `Optional<T> findAny()` — находит элемент в потоке.
- `long count()` — возвращает число элементов потока.
- `boolean allMatch(Predicate<T> predicate)` — возвращает истину, если все элементы **stream** удовлетворяют условию предиката.
- `boolean anyMatch(Predicate<T> predicate)` — возвращает истину, если хотя бы один элемент **stream** удовлетворяет условию предиката.
- `boolean noneMatch(Predicate<T> predicate)` — возвращает истину, если ни один элемент **stream** не удовлетворяет условию предиката.
- `Optional<T> reduce(T identity, BinaryOperator<T> accumulator)` — сводит все элементы потока к одному результирующему объекту, завернутому в оболочку `Optional` применяя функцию к результату применения функции к предидущим элементам и к следующему элементу.
- `<R, A> R collect(Collector<? super T, A, R> collector)` — собирает элементы в коллекцию или объект другого типа.
- `Optional<T> min(Comparator<T> comparator)` — находит минимальный элемент.
- `Optional<T> max(Comparator<T> comparator)` — находит максимальный элемент.