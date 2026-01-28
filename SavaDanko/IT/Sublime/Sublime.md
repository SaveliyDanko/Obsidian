## Создание своего Snippet
**Создание Snippets**
1. Откройте Sublime Text
2. Создайте новый файл snippet:
    - Перейдите в меню `Tools -> Developer -> New Snippet...`
3. Редактируйте шаблон snippet:
	По умолчанию вы увидите шаблон, который выглядит примерно так:
```xml
<snippet>
    <content><![CDATA[
Hello, ${1:this} is a ${2:snippet}.
]]></content>
    <!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
    <!-- <tabTrigger>hello</tabTrigger> -->
    <!-- Optional: Set a scope to limit where the snippet will trigger -->
    <!-- <scope>source.python</scope> -->
</snippet>
```


## My Snippets

**`public static void main`** 
```xml
<snippet>
    <content><![CDATA[
public static void main(String[] args) {
    $0
}
]]></content>
    <!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
    <tabTrigger>psvm</tabTrigger>
    <!-- Optional: Set a scope to limit where the snippet will trigger -->
    <scope>source.java</scope>
</snippet>
```

**`System.out.println()`**
```xml
<snippet>
    <content><![CDATA[
System.out.println("$0");
]]></content>
    <!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
    <tabTrigger>sout</tabTrigger>
    <!-- Optional: Set a scope to limit where the snippet will trigger -->
    <scope>source.java</scope>
</snippet>

```


## Sublime Packages
**Установка Package Control**
```
Tools -> Install Package Control 
```

