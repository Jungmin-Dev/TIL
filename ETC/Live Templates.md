<h1> Live Template </h1>

- IntelliJ는 Live Template 이라는 이름으로 이런 편리한 기능을 제공한다.
  - psvm
    - 이 상태에서 엔터를 입력하면, 아래와 같은 코드 스니펫이 자동으로 완성된다.
``` java
public static void main(String[] args) {

}

```

- sout, fori 등등 유용하게 사용할 수 있는 Live Template이 기본적으로 많이 제공되고 있다. 이런 편리한 Live Template을 우리가 직접 정의할수도 있다.


<h4> Live Template 커스텀 </h4>

- `맥` 기준으로 작성되었다.

- IntelliJ의 `Preferences > Editor > Live Templates` 메뉴로 들어가자. 그리고 여기서 자신이 사용할 언어를 선택하여 펼치자. 나는 Java를 선택하였다.

![image](https://user-images.githubusercontent.com/74536458/203461909-13f98a45-9f94-40ca-a6e9-6e8258e647bc.png)

- 우측의 + 버튼을 클릭하고, Live Template을 클릭한다.

![image](https://user-images.githubusercontent.com/74536458/203461926-c656ff88-7a7c-4aad-ba23-b07af5e1efac.png)

- Abbreviation에 단축어 이름을 입력하고, Description에 설명을 적는다. 그리고 좌측 하단 Define 버튼을 클릭하여, Live Template을 사용할 환경을 선택한다. 나는 Java를 선택했다.

- 마지막으로 Template Text에 코드 템플릿을 적어주면 된다. 이때, $로 텍스트를 감싸면 Live Template 변수로 사용할 수 있다. 나는 아래와 같이 작성했다.

```java
@org.junit.jupiter.api.Test
@DisplayName("$END$")
void $METHOD_NAME$() {
  // given

  // when

  // then
  org.assertj.core.api.Assertions.assertThat(1).isEqualTo(1)
}
```

모든 설정을 했다면 아래와 같이 만든 Live Template을 사용할 수 있다.
