---
title: 关于@bean注解的一点小探索
date: 2017-11-30 13:17:55
tags:
	- java
---

### 前言
最近看到@bean在方法上使用时，方法可以带参数，因此对其机制产生了一点好奇。 然后在网上搜索@bean，基本只讲其用法，而对特性没有涉及。最后终于在API说明中，略微了解了一点。

### 关于@bean在@Configuration标注的类中的特性

正常情况下，方法return的对象即被Spring作为一个单例bean管理。如果方法带有参数,则貌似参数会自动被装配，这一点，目前在任何文档上都没有说明。

如果在方法内部，调用了属于同一个类的其他被@bean的方法，相当于直接获取该bean,这被API文档称为 **inter-bean references**。其内部实际上是每个方法都通过```CGLIB```作了代理。

```

 @Configuration
 public class AppConfig {
 
     @Bean
     public FooService fooService() {
         return new FooService(fooRepository());
     }
 
     @Bean
     public FooRepository fooRepository() {
         return new JdbcFooRepository(dataSource());
     }
 
     // ...
 }
```

### 关于@Bean在@Component标注的类中的特性
API文档中，将@Bean运用在@Component类或普通类中的行为，称为**lite mode**。 这种场景下，@bean标注的方法，实际上可以被视为一个工厂方法.上文所述**inter-bean references**特性在这种场景下并不会生效，即方法本身不会使用CGLIB生成代理。
但方法参数列表中的参数，依然会被自动装配。

### 总结
虽然没有找到任何文档说明，但据推测，@bean注解首先有类似于@autowired注解的作用。其方法中的参数应该会在应用启动时，被bean工厂生成和注入。