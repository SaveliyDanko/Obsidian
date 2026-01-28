В Gradle подключение зависимостей делается через секцию `dependencies`, и по умолчанию Gradle использует репозиторий **Maven Central**, но можно подключить и другие.

#### Подключение репозиториев
[[3 repositories]]

#### Подключение зависимостей
В `dependencies` указываешь, что нужно подтянуть:
```groovy
dependencies {
    implementation 'com.google.code.gson:gson:2.10.1'
    testImplementation 'junit:junit:4.13.2'
}
```
Формат:  
`groupId:artifactId:version`

