<h1> Spring Boot War, Jar 생성 </h1>

<h2> Gradle build.gradle 설정 </h2>

build.gradle 설정 파일에 아래 코드 추가

`apply plugin: 'war'`

<h2> Application 설정 </h2>

- 해당 사항은 스프링부트 프로젝트 생성할 때 자동으로 만들어주기도 한다.

```

// BoardApplication 파일
@MapperScan(basePackages = {"jungmin.board.mapper"})
@SpringBootApplication(scanBasePackages = {"jungmin.board.config", "jungmin.board.controller" ,"jungmin.board.service" })
public class BoardApplication {


   public static void main(String[] args) {
      SpringApplication.run(BoardApplication.class, args);
   }

}

// ServletInitializer 파일
public class ServletInitializer extends SpringBootServletInitializer {

   @Override
   protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
      return application.sources(BoardApplication.class);
   }

}
```

<h2> war, jar 파일 생성 </h2>

![image](https://user-images.githubusercontent.com/74536458/179504059-ee64c605-0a6b-4713-b45a-d472ef6cdb98.png)
