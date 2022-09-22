<h1> 검증(Validation) </h1>

<h3> 1. Java Bean Validation (어노테이션 기반) </h3>

<h3> 2. Spring validator 인터페이스 구현을 통한 validation </h3>

 

<h3> Java Bean Validation </h3>

 -스프링 부트에서는 gradle에 의존성 하나만 추가해주면 간단하게 사용할 수 있다.

`implementation("org.springframework.boot:spring-boot-starter-validation")`

JavaBean 기반으로 간편하게 개별 데이터를 검증할 수 있으며, JavaBean내에 어노테이션으로 검증방법을 명시하면 된다. 

<h4> Validation의 주요 어노테이션 </h4>

- 회원가입을 위해 유저 정보를 담는 간단한 JavaBean을 생성하고 Validation을 적용하는 예시

```Java
public class MemberCreationRequest {
	@NotBlank(message="이름을 입력해주세요.")
	@Size(max=50, message="이름의 최대 길이는 50자 입니다.")
    	private String name;
	@Min(0, "나이는 0보다 커야 합니다.")
    	private int age;
	@Email("이메일 형식이 잘못되었습니다.")
    	private int email;
   // getter와 setter 생략
}
```

위처럼 DTO에 어노테이션으로 명시한 후 RequestBody에 @Valid 어노테이션을 달면 유효성 검증을 수행한 후 검증이 통과되었을 때에만 메서드 내부로 진입할 수 있고, 검증이 실패한다면 MethodArgumentNotValidException을 Throw를 던진다.

```Java
@PostMapping(value = "/member")
public MemeberCreationResponse createMember(
	@Valid @RequestBody MemeberCreationRequest memeberCreationRequest) {
	// 맴버 생성 로직 생략
}
```

1차적으로는 Java Bean Validation을 사용해서 DTO단에서 데이터를 간단하게 검증 하고나서, 로직으로 넘어왔을 때 2차적으로 권한, 서비스 정책, 경우에 따라서는 외부 API호출이나 DB 조회를 통한 데이터 검증을 실시하고 검증 실패시에는 Custom Exception으로 예외를 던지고 이를 처리하는 방식으로 검증을 진행하면 좀 더 확실한 Validation이 가능하다.

<h3> Spring Validator 인터페이스 구현 </h3>

- 유효성 검사를 수행하는 또다른 방법은 Validator 인터페이스를 구현하는 클래스를 생성하고 이를 스프링 빈으로 등록하는 방법

- Java Bean Validation에 비해서 조금 더 복잡한 로직을 갖는 유효성 검증이 가능하지만, Validation을 수행하는 클래스를 따로 정의하기 때문에 상대적으로 코드를 찾기 어렵고, 여러 군데 흩어져 있으면 테스트 및 유지보수가 어렵다는 단점이 있다.

```Java
@Component
public class PersonValidator implements Validator {
    public boolean supports(Class clazz) { // Validator를 동작시킬 조건
        return Person.class.equals(clazz);
    }
public void validate(Object obj, Errors e) { // 조건이 맞을 때 동작하게 될 Validation의 내용
        ValidationUtils.rejectIfEmpty(e, "name", "name.empty");
        Person p = (Person) obj;
        if (p.getAge() < 0) {
            e.rejectValue("age", "negativevalue");
        } else if (p.getAge() > 110) {
            e.rejectValue("age", "too.darn.old");
        }
    }
}
```

- 위에 정의된 Validator는 Person이라는 javaBean이 등록되어 있을 때, 해당 인스턴스에서만 활용되는 Validator다.

- supports 메서드는 이 validator가 동작할 조건을 정의하며(주로 class 타입을 비교) validate 메서드에서 원하는 검증을 진행하면 된다.


출처 : https://jhkimmm.tistory.com/6 [[SpringCore] Validation (유효성 검증)]
