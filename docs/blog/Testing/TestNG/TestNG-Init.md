# [TestNG 使用](https://www.yiibai.com/testng/hello-world-example.html)

## maven

```xml
<dependency>
  <groupId>org.testng</groupId>
  <artifactId>testng</artifactId>
  <version>6.8.7</version>
  <scope>test</scope>
</dependency>
<dependency>
  <groupId>junit</groupId>
  <artifactId>junit</artifactId>
  <version>3.8.1</version>
  <scope>test</scope>
</dependency>

```

## 概念

> TestNG按照官方的定义：
>
> **TestNG**是一个测试框架，其灵感来自JUnit和NUnit，但引入了一些新的功能，使其功能更强大，使用更方便。
>
> TestNG是一个开源自动化测试框架;TestNG表示**下一代**(**N**ext **G**eneration的首字母)。 TestNG类似于JUnit(特别是JUnit 4)，但它不是JUnit框架的扩展。它的灵感来源于JUnit。它的目的是优于JUnit，尤其是在用于测试集成多类时。 TestNG的创始人是**Cedric Beust**(塞德里克·博伊斯特)。
>
> TestNG消除了大部分的旧框架的限制，使开发人员能够编写更加灵活和强大的测试。 因为它在很大程度上借鉴了Java注解(JDK5.0引入的)来定义测试，它也可以显示如何使用这个新功能在真实的Java语言生产环境中。
>
> **TestNG的特点**
>
> - 注解
> - TestNG使用Java和面向对象的功能
> - 支持综合类测试(例如，默认情况下，不用创建一个新的测试每个测试方法的类的实例)
> - 独立的编译时测试代码和运行时配置/数据信息
> - 灵活的运行时配置
> - 主要介绍“测试组”。当编译测试，只要要求`TestNG`运行所有的“前端”的测试，或“快”，“慢”，“数据库”等
> - 支持依赖测试方法，并行测试，负载测试，局部故障
> - 灵活的插件API
> - 支持多线程测试



