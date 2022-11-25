<h1> GSON </h1>

- 구글에서 만든 자바 오브젝트의 직렬화/역직렬화 라이브러리이다.

<h3> GSON 라이브러리 추가하기(maven) </h3>

``` java
<dependency>
  <groupId>com.google.code.gson<groupId>
  <artifactId>gson</artifactId>
  <version>2.8.7</version>
</dependency>
```

<h3> Gson 객체 생성하기 </h3>

``` java
new Gson()
```

<h3> Map -> JSON, JSON -> Map  </h3>

``` java

Gson gsonObj = new Gson();
    
Map<String, String> inputMap = new HashMap<String, String>();
inputMap.put("name", "makesomething");
inputMap.put("blog", "https://web-inf.tistory.com");
        
// MAP -> JSON 예제
String jsonStr = gsonObj.toJson(inputMap);
System.out.println("MAP -> JSON 예제 : " + jsonStr);
        
// JSON -> MAP 예제
Map map = gsonObj.fromJson(jsonStr, Map.class);
System.out.println("JSON -> MAP 예제 : " + map.toString());

```

![image](https://user-images.githubusercontent.com/74536458/203700835-20685b71-d3e7-4ec3-a056-f52b8141f9ca.png)



<h3> JsonObject 만들기 </h3>

```java
// JsonObject 생성
JsonObject jsonObject = new JsonObject();
jsonObject.addProperty("name", "makesomething");
jsonObject.addProperty("blog", "http://web-inf.tistory.com");
jsonObject.addProperty("boolean", true);
jsonObject.addProperty("int", 12345);
        
System.out.println("JsonObject 생성 : " + jsonObject.toString() + "\n");
 
// String 리턴
System.out.println("JsonObject name(String) : " + jsonObject.get("name").getAsString());
System.out.println("JsonObject blog(String) : " + jsonObject.get("blog").getAsString());
 
// boolean 리턴
System.out.println("JsonObject boolean(boolean) : " + jsonObject.get("boolean").getAsBoolean());
 
// int 리턴
System.out.println("JsonObject int(int) : " + jsonObject.get("int").getAsInt());
```

![image](https://user-images.githubusercontent.com/74536458/203700952-68155f6d-b90b-4370-a0a4-13de5c5d1c06.png)


<h3> JsonArray 만들기 </h3>

```java

// JsonObject 생성
JsonObject jsonObject = new JsonObject();
jsonObject.addProperty("name", "makesomething");
jsonObject.addProperty("blog", "http://web-inf.tistory.com");
jsonObject.addProperty("boolean", true);
jsonObject.addProperty("int", 12345);
                
System.out.println("JsonObject 생성 : " + jsonObject.toString() + "\n");
        
// JsonArray 생성
JsonArray jsonArray = new JsonArray();
jsonArray.add(jsonObject);
        
System.out.println(jsonArray.toString());
    
// JsonArray 0번 index에있는 jsonObject의 name을 string으로 리턴
System.out.println(jsonArray.get(0).getAsJsonObject().get("name").getAsString());

```

<h3>  Gson Parse Pretty </h3>

```java

// JsonObject 생성
JsonObject jsonObject = new JsonObject();
jsonObject.addProperty("name", "makesomething");
jsonObject.addProperty("blog", "http://web-inf.tistory.com");
jsonObject.addProperty("boolean", true);
jsonObject.addProperty("int", 12345);
                
System.out.println("JsonObject 생성 : " + jsonObject.toString() + "\n");
        
// Parse Pretty
Gson gson = new GsonBuilder().setPrettyPrinting().create();
String jsonOutput = gson.toJson(jsonObject);
        
System.out.println(jsonOutput);

```

![image](https://user-images.githubusercontent.com/74536458/203701145-4c7882dc-f366-4251-b6de-512edc01b25e.png)

출처: https://web-inf.tistory.com/64
