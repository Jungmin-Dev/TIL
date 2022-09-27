<h1> 검증(Validation) </h1>

<h3> Bean Validation이란 </h3>

- 스프링에서 유효성 검증 로직을 구현하기 위한 사실상 표준

- 검사 대상 클래스에 어노테이션 기반 제약 조건을 선언하여 간결하게 유효성 검사가 가능하다.

- Bean Validation을 사용하려면 validation 의존 관계를 추가해야 한다.

`implementation 'org.springframework.boot:spring-boot-starter-validation'`

<h3> 검증 애노테이션 </h3>

- @NotBlank : 빈값 + 공백만 있는 경우를 허용하지 않는다.
- @NotNull : null 을 허용하지 않는다.
- @Range(min = 1000, max = 1000000) : 범위 안의 값이어야 한다.
- @Max(9999) : 최대 9999까지만 허용한다.

<h3> @NotNull, @NotEmpty, @NotBlank 의 차이점 </h3>

- @NotNull: Null만 허용하지 않는다. ""이나 " "은 가능하다.
- @NotEmpty: null 과 "" 둘 다 허용하지 않게 합니다. " "은 가능하다.
- @NotBlank: null 과 "" 과 " " 모두 허용하지 않습니다.

```java

@Data
public class ItemSaveForm {
   @NotBlank
    private String itemName;
    
    @NotNull @Range(min = 1000, max = 1000000)
    private Integer price;
    
    @NotNull @Max(value = 9999)
    private Integer quantity;
}
```

<h4> 검증 순서 </h4>

1. @ModelAttribute 각각의 필드에 타입 변환 시도
- 성공하면 다음으로
- 실패하면 `errorCode=typeMismatch`로 `FieldError` 추가

2. Validator 적용
- 즉, 바인딩에 성공한 필드만 Bean Validation을 적용한다.

<h3> 에러 코드 자동 생성 </h3>

- `MessageCodesResolver`를 통해 메시지 코드가 순서대로 생성된다.

1. 애노테이션.오브젝트.필드
2. 애노테이션.필드
3. 애노테이션.타입
4. 애노테이션


- @NotBlank
	- NotBlank.item.itemName
	- NotBlank.itemName
	- NotBlank.java.lang.String
	- NotBlank

- @Range
	- Range.item.price
	- Range.price
	- Range.java.lang.Integer
	- Range
	
<h3> 메시지 등록 </h3>

``` java
#errors.properties 추가
NotBlank={0} 공백X 
Range={0}, {2} ~ {1} 허용
Max={0}, 최대 {1}
```

- {0} 은 필드명이고, {1} , {2} ...은 각 애노테이션 마다 다르다

<h3> BeanValidation이 오류 메시지를 찾는 우선순위 </h3>

1. 생성된 메시지 코드 순서대로 `messageSource` 에서 메시지 찾기
2. 애노테이션의 message 속성 사용 `@NotBlank(message = "공백! {0}")`
3. 라이브러리가 제공하는 기본 값 사용

<h3> 오브젝트 오류 </h3>
- @ScriptAssert() 를 사용하면 된다.
- 그런데 실제 사용해보면 제약이 많고 복잡하다. 그리고 실무에서는 검증 기능이 해당 객체의 범위를 넘어서는 경우들도 종종 등장하는데, 그런 경우 대응이 어렵다.
- 따라서 @ScriptAssert() 보다는 자바 코드에서 **bindingResult.reject**를 사용하는것을 추천한다.

``` java
@PostMapping("/add")
public String addItem(@Validated @ModelAttribute Item item, BindingResult bindingResult, RedirectAttributes redirectAttributes) {
   //특정 필드 예외가 아닌 전체 예외
       if (item.getPrice() != null && item.getQuantity() != null) {
       int resultPrice = item.getPrice() * item.getQuantity();
       if (resultPrice < 10000) {
          bindingResult.reject("totalPriceMin", new Object[]{10000, resultPrice}, null);
       }
    }
    
    if (bindingResult.hasErrors()) {
       log.info("errors={}", bindingResult);
       return "/add";
    }
    
    //성공 로직
    Item savedItem = itemRepository.save(item);
    redirectAttributes.addAttribute("itemId", savedItem.getId());
    redirectAttributes.addAttribute("status", true);
   return "redirect:/items/{itemId}";
}
```

출처 : https://velog.io/@gmtmoney2357/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8-Bean-Validation - 스프링 부트 - 검증2: Bean Validation
