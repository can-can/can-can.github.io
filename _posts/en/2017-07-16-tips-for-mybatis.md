---
layout: post
title: Tips for Mybatis
categories: en
category: en

---

## 1. Mapper can not have two methods with same name, while using annotation to impelment Mapper
### Exmaple

The code below shows two methods with same name, using Java's overload, and can be compiled correctly.
~~~
public interface TestDAO {
    @Select("SELECT COUNT(id) FROM table WHERE id = #{id}")
    int select(@Param("id") int id);

    @Delete("SELECT COUNT(id) FROM table WHERE id = #{id} AND id2 = #{id2}")
    int select(@Param("id") int id, @Param("id2") int id2);
}

~~~

But, when running the code, this exception will be raised.
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

Why dose this exception be raised? Let us look source code. The code below is at `Configuration.java:655`. I find that MyBatis put `ms.getId()` as key into StrictMap，causing the exception above.
~~~
//at org.apache.ibatis.session.Configuration.addMappedStatement(Configuration.java:655)
public void addMappedStatement(MappedStatement ms) {
    mappedStatements.put(ms.getId(), ms);
}
~~~

Further, I dig source code and find two codes will generate the id of MappedStatement;
First one is at `XMLStatementBuilder:57`, `String id = context.getStringAttribute("id");`. This code show us that the id is excract from attribute named id in XML.
Second one is at `MapperAnnotationBuilder:292`, ` final String mappedStatementId = type.getName() + "." + method.getName();`. When generate Mapper by annotation, id of MappedStatement consists of class name and method name without arguments, so there will be raised exception when method name is duplicated
