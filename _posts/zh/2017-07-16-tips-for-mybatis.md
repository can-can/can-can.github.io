---
layout: post
title: Mybatis使用提示
categories: zh
category: zh
tag: MYBATIS DAO

---

## 1. 使用注解方式生成Mapper时，不能有重名方法
### 例子

下面使用了Java方法重载来实现了两个命为`select`方法。
~~~
public interface TestDAO {
    @Select("SELECT COUNT(id) FROM table WHERE id = #{id}")
    int select(@Param("id") int id);

    @Delete("SELECT COUNT(id) FROM table WHERE id = #{id} AND id2 = #{id2}")
    int select(@Param("id") int id, @Param("id2") int id2);
}

~~~

运行时会报这个异常。
~~~
Exception in thread "main" java.lang.IllegalArgumentException: Mapped Statements collection already contains value for dao.TestDAO.select
    at org.apache.ibatis.session.Configuration$StrictMap.put(Configuration.java:859)
    at org.apache.ibatis.session.Configuration$StrictMap.put(Configuration.java:831)
    at org.apache.ibatis.session.Configuration.addMappedStatement(Configuration.java:655)
    at org.apache.ibatis.builder.MapperBuilderAssistant.addMappedStatement(MapperBuilderAssistant.java:302)
    at org.apache.ibatis.builder.annotation.MapperAnnotationBuilder.parseStatement(MapperAnnotationBuilder.java:351)
    at org.apache.ibatis.builder.annotation.MapperAnnotationBuilder.parse(MapperAnnotationBuilder.java:134)
    at org.apache.ibatis.binding.MapperRegistry.addMapper(MapperRegistry.java:72)
    at org.apache.ibatis.session.Configuration.addMapper(Configuration.java:728)
~~~

原因是什么呢？我们从源码来看一下。下面是`Configuration.java:655`这行代码。我们发现Myatis将`ms.getId()`当作key放到了StrictMap中，从而导致了StrictMap抛出异常。
~~~
//at org.apache.ibatis.session.Configuration.addMappedStatement(Configuration.java:655)
public void addMappedStatement(MappedStatement ms) {
    mappedStatements.put(ms.getId(), ms);
}
~~~

继续查找源码发现有两个地方生成MappedStatement的id。
第一个是`XMLStatementBuilder:57`，`String id = context.getStringAttribute("id");`。是XML解析的时候，获取id属性上的字符串来作为key。
第二个是`MapperAnnotationBuilder:292`,` final String mappedStatementId = type.getName() + "." + method.getName();`。是通过注解生成Mapper时，将Mapper类名加上方法名作为id，并没有将方法参数作为id的一部分，所以导致了上述异常。
