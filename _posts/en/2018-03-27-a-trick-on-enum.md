---
layout: post
title: A trick on enum
categories: en
category: en

---

#My situation
My Java version is  7.
I receive a list of String like the code below. The count of String is up to 50.
```
cityid
username
...
```
also, I have class
```
class Data{
  private boolean cityId;
  private boolean userName
  //setters
}
```
Now, I need set field true if the list contains the field.
You may noticed that The Strings in the list have the same meaning with fields in the class, but fields use Camel-Case.

# First solution
```
for(String name :  list){
    if(name.equals("cityid"){
        data.setCityId(true);
    }else if(name.equals("username"){
        data.setUserName(true);
    }
}
```
This solution works for which has few fields. However, It is not elegant for 50 fields.

# Interface solution
```
interface Setter{
      void setTrue(Data data)
}

class CityIdSetter extend Setter{
    @Override
    void setTrue(Data data){
        data.setCityId(true);
    }
}


class UserNameSetter extend Setter{
    @Override
    void setTrue(Data data){
        data.setUserName(true);
    }
}

class Main{
    static Map<String,Setter> map;
    static{
        map.put("cityId", new CityIdSetter());
        map.put("username", new UserNameSetter());
    }
    public static int main(String[] args){
       
        Data data;
        for(String name :  list){
            Setter setter = map.get(name);
            if(setter != null){
                 setter.setTrue(data)
            }
        }
    }
}
```
This code is more elegant, still too many.

# Enum solution
My final solution is using enum to initialize Setter and to map field.

```
enum Setter{
 cityid{
    @Override
    void setTrue(Data data){
        data.setCityId(true);
    }
 }
 
 username{
    @Override
    void setTrue(Data data){
        data.setUserName(true);
    }
 }
abstract void setTrue(Data data);

}

class Main{

    public static int main(String[] args){
       
        Data data;
        for(String name :  list){
            Setter setter = Setter.valueOf(name);
            if(setter != null){
                 setter.setTrue(data)
            }
        }
    }
}
```

