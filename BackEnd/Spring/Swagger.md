<h1>Swagger 라이브러리</h1>

- 서버로 요청되는 API리스트를 HTML 화면으로 문서화하여 테스트 할 수 있는 라이브러리
- 서버가 가동하면서 @RestController를 읽어 API를 분석하여 HTML 문서를 작성함<br>
<b> REST API의 스펙을 문서화 하는것은 매우 중요 </b>
<br>
- 기존 Swagger를 사용하지 않을 때는 API를 변경할 때마다 Reference 문서를 계속 바꿔야하는 불편함 존재

<h2> Swagger 설정 </h2>

<h3> build.gradle 설정 </h3>
   
```java
   // Swagger 관련 설정
   implementation 'io.springfox:springfox-boot-starter:3.0.0'
```

<h3> SwaggerConfig 설정 </h3>

```java
@Configuration
@EnableSwagger2
public class SwaggerConfig {
    @Bean
    public Docket api() {
        return new Docket(DocumentationType.OAS_30)
                .useDefaultResponseMessages(false)
                .select()
                .apis(RequestHandlerSelectors.basePackage("jungmin.board.controller"))
                .paths(PathSelectors.any())
                .build();
    }
}
```

- Docket: Swagger 설정의 핵심이 되는 Bean
- useDefaultResponseMessages: Swagger 에서 제공해주는 기본 응답 코드 (200, 401, 403, 404). true 로 설정하면 기본 응답 코드를 노출
- apis: api 스펙이 작성되어 있는 패키지 (Controller) 를 지정
- paths: apis 에 있는 API 중 특정 path 를 선택


<h3> 어노테이션 </h3>

- @Api(value="", tags=""): 해당 클래스가 Swagger 리소스임을 명시<br>
value: 사용자 지정 이름 기재, tags사용 시, 무시되게 된다.<br>
tags: 태그에 여러 이름을 콤마(,) 단위로 기재 시, 여러 태그 정의 가능<br>

- @ApiOperation(value="", notes=""): 해당 api에 대한 명세<br>
value: 현재 api에 대한 정의<br>
notes: 현재 api에 대한 Comment<br>

- @ApiParam(value="", required="", example=""): 파라미터에 대한 명세<br>
value: 현재 파라미터에 대한 설명<br>
required: 필수 여부<br>
example: 파라미터 예시<br>

> 2.9.2 버전<br>
localhost:포트/swagger-ui.html 접속하여 확인<br>

> 3x 버전 이상<br>
localhost:8080/swagger-ui/index.html

<h2>결과 화면</h2>

![image](https://user-images.githubusercontent.com/74536458/175575782-d58b1c38-c104-45e0-8141-df937a3b7c1c.png)


출처 : https://velog.io/@cho876/API-Swagger-%EC%82%AC%EC%9A%A9%EB%B2%95


