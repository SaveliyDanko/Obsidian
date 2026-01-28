В `build.gradle` указываются репозитории:
```groovy
repositories {
    mavenCentral() // основной источник
    google()       // часто используется в Android проектах
    maven { url 'https://jitpack.io' } // кастомный репозиторий
}
```