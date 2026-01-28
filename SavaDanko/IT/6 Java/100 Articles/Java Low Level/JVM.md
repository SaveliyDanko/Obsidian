**Class Loading Subsystem**
- [ ] Нарушение делегирования (OSGi, плагинные системы).
- [ ] Unloading классов
- [ ] Class redefinition / instrumentation
- [ ] Class File Format

**Runtime Data Areas**
- [ ] Метасегменты памяти
- [ ] Потоки и память

- [ ] Java Virtual Machine Specification
- [ ] Stack-based vs. register-based архитектуры

---

## 🔹 2. Архитектура JVM

1. **Общие компоненты**
    - Execution Engine.
        
    - Native Interface (JNI).
        
    - Garbage Collector.


---

## 🔹 5. Execution Engine

1. **Интерпретатор**
    
    - Построчное выполнение байткода.
        
2. **JIT-компиляция**
    
    - C1 (Client), C2 (Server), Graal JIT.
        
    - Tiered Compilation.
        
3. **HotSpot (Adaptive Optimization)**
    
    - Профилирование методов, инлайнинг, оптимизация ветвлений.
        
4. **Optimization Techniques**
    
    - Escape Analysis, Loop Unrolling, Dead Code Elimination, Lock Coarsening, Devirtualization.
        
5. **AOT-компиляция**
    
    - GraalVM Native Image.
        
    - Преимущества и ограничения.
        
6. **InvokeDynamic и Lambda**
    
    - Как работает динамическое связывание методов.
        
    - LambdaMetaFactory.
        

---

## 🔹 6. Байткод и его выполнение

1. **Формат байткода**
    
    - Однобайтовые инструкции.
        
    - Работа со стеком.
        
2. **Основные инструкции**
    
    - Загрузка/сохранение (load/store), арифметика, ветвления, вызов методов.
        
3. **Профилировка и байткод**
    
    - Как JVM определяет «горячие» методы.
        
4. **Инструменты анализа байткода**
    
    - `javap`, ASM, BCEL, ByteBuddy.
        

---

## 🔹 7. Garbage Collection (GC)

1. **Общие понятия**
    
    - Что такое сборка мусора, зачем нужна.
        
    - Reachability: GC Roots, strong/weak/phantom references.
        
2. **Алгоритмы GC**
    
    - Serial GC.
        
    - Parallel GC.
        
    - CMS (устаревший).
        
    - G1 GC.
        
    - ZGC.
        
    - Shenandoah.
        
3. **Фазы GC**
    
    - Mark → Sweep → Compact.
        
    - Copying (для Young Gen).
        
    - Stop-The-World.
        
4. **Поколенческая модель памяти**
    
    - Young, Old, Perm/Metaspace.
        
5. **Тюнинг GC**
    
    - `-Xms`, `-Xmx`, `-XX:+UseG1GC`, `-XX:MaxGCPauseMillis`.
        
6. **GC Logging & инструменты анализа**
    - `-Xlog:gc*`, `GCEasy`, `JClarity`, `VisualVM`.
        

---

## 🔹 8. Java Memory Model (JMM) и многопоточность

1. **Java Memory Model (JMM)**
    
    - Абстракция памяти, доступ между потоками.
        
    - Happens-before.
        
2. **Ключевые элементы JMM**
    
    - `volatile`, `synchronized`, final, atomicity/visibility/ordering.
        
3. **Инструкции процессора и reordering**
    
    - Memory Barriers, CPU cache coherence.
        
4. **Синхронизация и блокировки**
    
    - Мониторы, intrinsic locks.
        
    - Lightweight Locking, Biased Locking.
        
5. **Concurrent API и потоки**
    
    - Thread, Runnable, Callable, Future.
        
    - Fork/Join, Executors.
        
    - `java.util.concurrent`: Locks, Atomic, Latches.
        
6. **Deadlocks и race conditions**
    
    - Примеры и детекция (`jstack`, VisualVM).
        

---

## 🔹 9. Security в JVM

1. **Bytecode Verification**
    
    - Проверка валидности `.class` файлов.
        
    - Отказ от выполнения некорректного байткода.
        
2. **Security Manager (до Java 17)**
    
    - `java.policy` файлы.
        
    - Ограничения доступа к ресурсам.
        
3. **Sandboxing**
    
    - Ограниченные права, плагинные архитектуры.
        
4. **ClassLoader Security**
    
    - Проверка источников, namespace isolation.
        
5. **Cryptography APIs**
    
    - JCA/JCE, KeyStore, SecureRandom.
        

---

## 🔹 10. Native Interface (JNI)

1. **Зачем нужен JNI**
    
    - Вызов C/C++ кода из Java.
        
    - Работа с низкоуровневыми API.
        
2. **JNI API**
    
    - Метод `native`, генерация `.h` файлов.
        
    - `System.loadLibrary()`.
        
3. **Безопасность JNI**
    
    - Риски: утечки памяти, краши JVM.
        
4. **Альтернативы JNI**
    
    - JNA, Panama (в будущем).
        

---

## 🔹 11. Мониторинг и инструменты

1. **Инструменты командной строки**
    
    - `jps`, `jstat`, `jmap`, `jstack`, `jcmd`, `jinfo`.
        
2. **Визуальные инструменты**
    
    - VisualVM, JConsole, Java Mission Control (JMC), Flight Recorder.
        
3. **Heap Dump, Thread Dump**
    
    - Как снять и проанализировать.
        
4. **JFR (Java Flight Recorder)**
    
    - Event-based профилировка, минимальное влияние.
        
5. **Системы мониторинга**
    
    - Prometheus + JMX, Grafana dashboards.
        

---

## 🔹 12. Внутренние API JVM

1. **sun.misc.Unsafe**
    
    - Прямой доступ к памяти, CAS, off-heap allocation.
        
2. **VarHandles (Java 9+)**
    
    - Безопасная альтернатива Unsafe.
        
3. **Метод-хендлы и `invokeDynamic`**
    
    - Метод-хендлы, Lambda, динамические вызовы.
        
4. **VM Options и флаги**
    
    - `-XX:+UnlockExperimentalVMOptions`, `-Xlog`, `-XX:+PrintCompilation`.
        
5. **JEPs, влияющие на JVM**
    
    - Список JEP, улучшающих производительность, безопасность, GC, JIT.
        

---

## 🔹 13. JVM и современные технологии

1. **JVM и микросервисы**
    
    - Проблема долгого старта, потребление памяти.
        
    - AOT, GraalVM.
        
2. **JVM в Docker/Kubernetes**
    
    - Ограничение ресурсов (CPU, RAM), `UseContainerSupport`.
        
3. **JVM в serverless / FaaS**
    
    - Оптимизация cold start.
        
4. **Polyglot (многоязычность)**
    
    - Kotlin, Scala, Groovy, JRuby, Clojure.
        
    - GraalVM как polyglot runtime.
        
5. **JVM в embedded**
    
    - Compact Profiles, SubstrateVM.
        

---

## 🔹 14. Будущее JVM

1. **Релизный цикл Java**
    
    - Каждые 6 месяцев: JEP, LTS, non-LTS.
        
2. **Проекты внутри OpenJDK**
    
    - **Project Loom** — виртуальные потоки.
        
    - **Project Valhalla** — inline-классы / value types.
        
    - **Project Panama** — нативные вызовы без JNI.
        
    - **Project Leyden** — ускорение старта.
        
    - **Project Amber** — упрощение синтаксиса языка.
        
3. **Эволюция JIT/AOT**
    
    - Graal JIT, Graal Native Image.
        
4. **JVM как универсальная платформа**
    
    - Поддержка многих языков, embedded, real-time.
        

---

## 🔹 15. Практические аспекты и рекомендации

1. **Настройка JVM под продакшн**
    
    - GC параметры, heap tuning, логгирование.
        
2. **Диагностика ошибок**
    
    - OutOfMemoryError, StackOverflowError, GC overhead limit.
        
3. **Performance tuning**
    
    - Thread contention, heap size, JIT logs.
        
4. **Best practices**
    
    - Безопасная работа с памятью.
        
    - Эффективное использование потоков.
        
    - Понимание GC-пауз и логирования.
        

---

## 🔹 16. JVM: Ресурсы и документация

1. **Java Virtual Machine Specification**
    
2. **JEP Index**
    
3. **OpenJDK source**
    
4. **HotSpot Internals Wiki**
    
5. **JVM блогеры и эксперты**
    
    - Aleksey Shipilev, Monica Beckwith, Doug Lea и др.
        

---

Хочешь — я могу превратить этот план в шаблон статьи (Markdown, LaTeX, Notion), разбить на этапы написания или разработать оглавление книги на его основе. Как тебе будет удобнее продолжить?