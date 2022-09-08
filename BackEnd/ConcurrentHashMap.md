<h1> 동기화 ConcurrentHashMap </h1>

<h3> ConcurrentHashMap </h3>

<h4> 특징 </h4>

- HashMap과 다르게 key, value에 null을 허용하지 않는다.

- 멀티 쓰레드 환경에서는 ConcurrentUtil이 제공하는 ConcurrentHashMap 클래스를 사용하는 추세

- ConcurrentHashMap은 동기화 시, Map 전체에 동기화 락을 걸지 않고, Map을 여러 조각으로 쪼개어 부분부분 락을 거는 형태로 구현되어 있기 때문에 속도가 빠르다

- 그러한 이유로 특히 (멀티 쓰레드 환경에서) 쓰레드 간의 경쟁이 심한 경우, 훨씬 더 효율적인 성능이 보인다.

- 단일 쓰레드 환경이라면 그냥 HashMap을, 멀티쓰레드 환경이라면 ConcurrentHashMap 을 쓰면 된다

<h4> 추 후 조금 더 살펴보아야 하는 부분이다. </h4>

출처: https://ooz.co.kr/71 [이러쿵저러쿵:티스토리]
