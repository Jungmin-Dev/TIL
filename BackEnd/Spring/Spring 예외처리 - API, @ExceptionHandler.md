<h1> Spring 예외처리 - API, @ExceptionHandler </h1>

<h3> @ControllerAdvice를 이용한 API 예외처리 </h3> 

- Spring AOP에서 제공해주는 `@ControllerAdvice`, `@RestControllerAdvice` 를 이용하면 된다.
- `@RestControllerAdvice`는 그냥 기존태그에 `@ResponseBody`가 추가로 붙어있는 태그이다. 즉 return을 했을 때 뷰리졸버가 동작하지 않는다.

- 📑 ErrorResult  📑 ExControllerAdvice ➡  @ExceptionHandler 부분의 코드를 분리해 따로 작성한다.

```java
@Data
@AllArgsConstructor
public class ErrorResult {
    private String code;
    private String message;
}
```

```java
@Slf4j
@RestControllerAdvice(basePackages = "hello.exception.api")
public class ExControllerAdvice {
 
  @ResponseStatus(HttpStatus.BAD_REQUEST)
  @ExceptionHandler(IllegalArgumentException.class)
  public ErrorResult illegalExHandler(IllegalArgumentException e) {
    log.error("[exceptionHandler] ex", e);
    return new ErrorResult("BAD", e.getMessage());
  }
 
  @ExceptionHandler
  public ResponseEntity<ErrorResult> userExHandler(UserException e) {
    log.error("[exceptionHandler] ex", e);
    ErrorResult errorResult = new ErrorResult("USER-EX", e.getMessage());
    return new ResponseEntity(errorResult, HttpStatus.BAD_REQUEST);
  }
 
  @ResponseStatus(HttpStatus.INTERNAL_SERVER_ERROR)
  @ExceptionHandler
  public ErrorResult exHandler(Exception e) {
    log.error("[exceptionHandler] ex", e);
    return new ErrorResult("EX", "내부 오류");
  }
 
}
```

- (basePackages ="...")를 지정해주면 해당 패키지안에 있는 모든 @Controller에 적용된다.
- 따로 적지않는다면 프로젝트 경로에 있는 모든 컨트롤러에 적용된다. (Spring 공식문서)

- 이를 사용하면 이제 컨트롤러에서 예외코드를 작성하지 않아도 된다. 객체의 책임이 분리되었다. 

``` java
@Slf4j
@RestController
public class ApiExceptionV3Controller {
 
  @GetMapping("/api3/members/{id}")
  public MemberDto getMember(@PathVariable("id") String id) {
 
    if (id.equals("ex")) {
      throw new RuntimeException("잘못된 사용자");
    }
    if (id.equals("bad")) {
      throw new IllegalArgumentException("잘못된 입력 값");
    }
    if (id.equals("user-ex")) {
      throw new UserException("사용자 오류");
    }
 
    return new MemberDto(id, "hello " + id);
  }
}
 
// 참고로 MemberDto는 이렇게 생겼다.
@Data
@AllArgsConstructor
class MemberDto {
 
  private String memberId;
  private String name;
}
```
