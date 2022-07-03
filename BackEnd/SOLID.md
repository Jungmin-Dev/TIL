<h1>SOLID</h2>

- 클린코드로 유명한 로버트 마틴이 좋은 객체 지향 설계의 5가지 원칙을 정리

1. SRP: 단일 책임 원칙(single responsibility principle)<br>
 -> 하나의 모듈은 한 가지 책임을 가져야 한다는 것<br>
 -> 모듈이 변경되는 이유가 한가지여야 함<br>
2. OCP: 개방-폐쇄 원칙 (Open/closed principle)<br>
 -> 확장에 대해 열려있고 수정에 대해서는 닫혀있어야 한다는 원칙<br>
 -> 개방 폐쇄 원칙을 지키기 위해서는 추상화에 의존<br>
3. LSP: 리스코프 치환 원칙 (Liskov substitution principle)<br>
 -> 상위 타입이 하위 타입으로 변경되어도, 차이점을 인식하지 못한 채 상위 타입의 퍼블릭 인터페이스를 통해 서브 클래스를 사용할 수 있어야 한다는 것<br>
4. ISP: 인터페이스 분리 원칙 (Interface segregation principle)<br>
 -> 목적과 관심이 각기 다른 클라이언트가 있다면 인터페이스를 통해 적절하게 분리<br>
 -> 클라이언트의 목적과 용도에 적합한 인터페이스 만을 제공<br>
5. DIP: 의존관계 역전 원칙 (Dependency inversion principle)<br>
 -> 추상화에 의존하며 구체화에는 의존하지 않는 설계 원칙<br>
 
 <br>
 자세한 사항은 아래 출처 확인
<br>
출처: https://mangkyu.tistory.com/194 [MangKyu's Diary:티스토리]
