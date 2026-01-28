#java 

---
[[Runnable]]

---
A _thread_ is a thread of execution in a program. The Java virtual machine allows an application to have multiple threads of execution running concurrently.

`Thread` defines constructors and a `Thread.Builder` to create threads. Starting a thread schedules it to execute its `run` method. The newly started thread executes concurrently with the thread that caused it to start.

A thread _terminates_ if either its `run` method completes normally, or if its `run` method completes abruptly and the appropriate uncaught exception handler completes normally or abruptly. With no code left to run, the thread has completed execution. The `join` method can be used to wait for a thread to terminate.

Threads have a unique identifier and a name. The identifier is generated when a `Thread` is created and cannot be changed. The thread name can be specified when creating a thread or can be changed at a later time.

Threads support `ThreadLocal` variables. These are variables that are local to a thread, meaning a thread can have a copy of a variable that is set to a value that is independent of the value set by other threads. `Thread` also supports `InheritableThreadLocal` variables that are thread local variables that are inherited at thread creation time from the parent `Thread`. `Thread` supports a special inheritable thread local for the thread context-class-loader.

#### Platform Thread
`Thread` supports the creation of _platform threads_ that are typically mapped 1:1 to kernel threads scheduled by the operating system. Platform threads will usually have a large stack and other resources that are maintained by the operating system. Platforms threads are suitable for executing all types of tasks but may be a limited resource.

Platform threads get an automatically generated thread name by default.

Platform threads are designated _daemon_ or _non-daemon_ threads. When the Java virtual machine starts up, there is usually one non-daemon thread (the thread that typically calls the application's `main` method). The shutdown sequence begins when all started non-daemon threads have terminated. Unstarted non-daemon threads do not prevent the shutdown sequence from beginning.

In addition to the daemon status, platform threads have a thread priority and are members of a thread group.

#### Virtual Threads
`Thread` также поддерживает создание **виртуальных потоков**. Виртуальные потоки, как правило, являются **пользовательскими потоками** (_user-mode threads_), управляемыми средой выполнения Java, а не операционной системой. Обычно они требуют минимальных ресурсов, и одна виртуальная машина Java может поддерживать **миллионы виртуальных потоков**. Виртуальные потоки хорошо подходят для выполнения задач, которые большую часть времени находятся в состоянии ожидания, например, при операциях ввода-вывода. **Виртуальные потоки не предназначены для продолжительных и ресурсоёмких вычислений на CPU.**

Виртуальные потоки, как правило, используют небольшое количество платформенных потоков, называемых **несущими потоками** (_carrier threads_). Примерами операций, при которых несущий поток может быть переназначен от одного виртуального потока к другому, являются блокировки и операции ввода-вывода. Код, выполняющийся внутри виртуального потока, **не осведомлён** о том, на каком несущем потоке он исполняется. Метод `currentThread()`, используемый для получения ссылки на **текущий поток**, **всегда возвращает объект `Thread`, представляющий именно виртуальный поток**.

Виртуальные потоки по умолчанию не имеют имени. Метод `getName` возвращает пустую строку, если имя потока не было задано.

Виртуальные потоки являются **потоками-демонами**, поэтому они **не препятствуют** началу процесса завершения работы виртуальной машины. У виртуальных потоков **фиксированный приоритет**, который **нельзя изменить**.

#### Inheritance when creating threads
Поток `Thread`, созданный с помощью одного из публичных конструкторов, **наследует статус демона** и **приоритет потока** от родительского потока **в момент создания дочернего потока**. Также **группа потоков наследуется**, если она явно не указана в конструкторе.

При использовании `Thread.Builder` для создания платформенного потока статус демона, приоритет и группа потоков **также наследуются**, если они не заданы в билдере. Как и в случае с конструкторами, **наследование происходит в момент создания дочернего потока**.

Поток `Thread` наследует **начальные значения переменных `InheritableThreadLocal`** (включая **контекстный загрузчик классов**) от родительского потока **в момент создания дочернего потока**.

Для создания потока, **который не наследует** эти значения от потока-создателя, можно использовать **конструктор с пятью параметрами**.

При использовании `Thread.Builder` можно воспользоваться методом `inheritInheritableThreadLocals`, чтобы **явно указать**, должны ли наследоваться начальные значения `InheritableThreadLocal`.

---
###### **Thread**
```java
public Thread()
```
Инициализирует новый платформенный поток (`Thread`). Этот конструктор эквивалентен вызову `Thread(null, null, gname)`, где `gname` — автоматически сгенерированное имя. Автоматически сгенерированные имена имеют форму `"Thread-" + n`, где `n` — целое число.

Этот конструктор имеет смысл использовать только при наследовании от класса `Thread` с переопределением метода `run()`.

###### **Thread**
```java
public Thread(Runnable task)
```
`task` - the object whose `run` method is invoked when this thread is started. If `null`, this classes `run` method does nothing.

###### **Thread**
```java
public Thread(ThreadGroup group,
						Runnable task,
						String name,
						long stackSize,
						boolean inheritInheritableThreadLocals)
```
- `group` — группа потоков. Если указано `null`, потоку будет назначена группа текущего потока.
- `task` — объект, чей метод `run` будет выполнен при запуске потока. Если указано `null`, будет выполнен метод `run` самого потока.
- `name` — имя нового потока.
- `stackSize` — желаемый размер стека для нового потока. Если указано `0`, этот параметр игнорируется.
- `inheritInheritableThreadLocals` — если `true`, поток унаследует начальные значения всех наследуемых переменных потока от потока-родителя. Если `false`, значения не наследуются.

###### **currentThread**
```java
public static Thread currentThread()
```
Returns the Thread object for the current thread.

###### **yield**
```java
public static void yield()
```
Подсказка планировщику, что текущий поток готов уступить своё текущее использование процессора. Планировщик вольен проигнорировать эту подсказку.

Вызов `yield` является эвристической попыткой улучшить относительное продвижение потоков, которые в противном случае могли бы чрезмерно загружать процессор. Его использование следует сочетать с профилированием и бенчмаркингом, чтобы убедиться, что оно действительно даёт желаемый эффект.

Этот метод редко бывает уместным. Он может быть полезен для отладки или тестирования, где помогает воспроизвести ошибки, связанные с состояниями гонки. Также он может быть полезен при разработке низкоуровневых механизмов управления конкурентностью, таких как конструкции из пакета `java.util.concurrent.locks`.

###### **sleep**
```java
public static void sleep(long millis)
                  throws InterruptedException
```
Приостанавливает выполнение текущего потока на указанное количество миллисекунд, с учётом точности и разрешающей способности системных таймеров и планировщика задач.  
При этом поток не теряет владения какими-либо мониторами (то есть не освобождает захваченные блокировки).

###### **onSpinWait**
```java
public static void onSpinWait()
```
Указывает, что вызывающий поток временно не может продолжить выполнение, пока не произойдут определённые действия со стороны других потоков.

Вызывая этот метод внутри каждой итерации цикла активного ожидания (spin-wait loop), поток сообщает среде выполнения, что он находится в режиме активного ожидания.

Среда выполнения может предпринять меры для оптимизации производительности таких конструкций циклов активного ожидания.

```java
public class SpinWaitExample {

    private static volatile boolean ready = false;

    public static void main(String[] args) {

        Thread producer = new Thread(() -> {
            try {
                Thread.sleep(1000); // Имитация какой-то работы
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
            ready = true; // Устанавливаем флаг
            System.out.println("Producer: ready set to true");
        });

        Thread consumer = new Thread(() -> {
            System.out.println("Consumer: waiting for ready...");

            // Активное ожидание
            while (!ready) {
                Thread.onSpinWait(); // Подсказка JVM, что это активное ожидание
            }

            System.out.println("Consumer: detected ready == true");
        });

        producer.start();
        consumer.start();
    }
}
```

###### **ofPlatform**
```java
public static Thread.Builder.OfPlatform ofPlatform()
```
Returns a builder for creating a platform `Thread` or `ThreadFactory` that creates platform threads.

Запуск потока с `Runnable`
```java
public class Example1 {
    public static void main(String[] args) {
        Thread t = Thread.ofPlatform().start(() -> {
            System.out.println("Платформенный поток: " + Thread.currentThread());
        });

        System.out.println("Main поток: " + Thread.currentThread());
    }
}

```

Сначала создать, потом стартовать
```java
public class Example2 {
    public static void main(String[] args) {
        Runnable task = () -> System.out.println("Поток выполнен: " + Thread.currentThread().getName());

        Thread thread = Thread.ofPlatform().name("MyPlatformThread").unstarted(task);

        System.out.println("Создан поток: " + thread.getName());

        thread.start();
    }
}
```
###### **ofVirtual**
```java
public static Thread.Builder.OfVirtual ofVirtual()
```
Returns a builder for creating a virtual `Thread` or `ThreadFactory` that creates virtual threads.

###### **clone**
```java
protected Object clone()
                throws CloneNotSupportedException
```

###### **startVirtualThread**
```java
public static Thread startVirtualThread(Runnable task)
```
Creates a virtual thread to execute a task and schedules it to execute.

###### **isVirtual**
```java
public final boolean isVirtual()
```
Returns true if this thread is a virtual thread. A virtual thread is scheduled by the Java virtual machine rather than the operating system.

###### **start**
```java
public void start()
```
Schedules this thread to begin execution. The thread will execute independently of the current thread.
A thread can be started at most once. In particular, a thread can not be restarted after it has terminated.

###### **run**
```java
public void run()
```
Этот метод выполняется потоком при его запуске. Подклассы `Thread` могут переопределять этот метод.

Метод не предназначен для прямого вызова.  
Если поток является платформенным потоком, созданным с задачей `Runnable`, то вызов этого метода приведёт к вызову метода `run()` этой задачи.  
Если же поток является виртуальным, то прямой вызов этого метода не имеет никакого эффекта.

###### **interrupt**
```java
public void interrupt()
```
Прерывает выполнение этого потока.

Если поток заблокирован во время вызова одного из методов `wait()`, `wait(long)`, `wait(long, int)` класса `Object` или методов `join()`, `join(long)`, `join(long, int)`, `sleep(long)` или `sleep(long, int)` этого класса, то его статус прерывания будет сброшен, и поток получит исключение `InterruptedException`.

Если поток заблокирован во время выполнения операции ввода-вывода на объекте типа `InterruptibleChannel`, то канал будет закрыт, статус прерывания будет установлен, и поток получит исключение `ClosedByInterruptException`.

Если поток заблокирован при работе с селектором (`Selector`), то его статус прерывания будет установлен, и метод выбора завершится немедленно — возможно, с ненулевым значением — так, как если бы был вызван метод `wakeup()` селектора.

Если ни одно из вышеуказанных условий не выполнено, то будет просто установлен статус прерывания потока.

Прерывание потока, который не является активным, может не иметь никакого эффекта.

Прерывание `Thread.sleep()`
```java
public class InterruptExample1 {
    public static void main(String[] args) {
        Thread t = new Thread(() -> {
            try {
                System.out.println("Засыпаю...");
                Thread.sleep(5000);
                System.out.println("Проснулся");
            } catch (InterruptedException e) {
                System.out.println("Поток прерван во сне!");
            }
        });

        t.start();
        try {
            Thread.sleep(1000); // даем потоку время заснуть
        } catch (InterruptedException ignored) {}

        t.interrupt(); // прерываем поток
    }
}
```

###### **interrupted**
```java
public static boolean interrupted()
```
Проверяет флаг текущего потока и сбрасывает его

###### **isInterrupted**
```java
public boolean isInterrupted()
```
Проверяет флаг у вызываемого потока и не сбрасывает его

###### **isAlive**
```java
public final boolean isAlive()
```
Tests if this thread is alive. A thread is alive if it has been started and has not yet terminated.

###### **join**
```java
public final void join()
                throws InterruptedException
```
Waits for this thread to terminate.
###### **join**
```java
public final void join(long millis)
                throws InterruptedException
```
Waits at most millis milliseconds for this thread to terminate. A timeout of 0 means to wait forever. This method returns immediately, without waiting, if the thread has not been started.

###### **setPriority**
```java
public final void setPriority(int newPriority)
```
Changes the priority of this thread.

###### **getPriority**
```java
public final int getPriority()
```
Returns this thread's priority. 

###### **setName**
```java
public final void setName(String name)
```
Changes the name of this thread to be equal to the argument name.

###### **getName**
```java
public final String getName()
```
Returns this thread's name.

###### **getThreadGroup**
```java
public final ThreadGroup getThreadGroup()
```
Returns the thread's thread group or null if the thread has terminated. 

###### **setDaemon**
```java
public final void setDaemon(boolean on)
```
Marks this thread as either a daemon or non-daemon thread.

###### **isDaemon**
```java
public final boolean isDaemon()
```
Tests if this thread is a daemon thread. The daemon status of a virtual thread is always true.

###### **getState**
```java
public Thread.State getState()
```
