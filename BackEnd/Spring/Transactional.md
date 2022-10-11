<h1> 트랜잭션 </h1>

- DB에서 상태변화의 한 주기를 의미한다.
- 쉽게 말해서 바로 이전 커밋 이후의 작업부터, 이런저런 작업 후 최종적으로 커밋을 날리기까지의 주기이다.

<h4> @Transactional 어노테이션은, 해당 어노테이션이 적용되는 메소드를 하나의 트랜잭션으로 묶어주는 역할을 한다. </h4>

<h3> 트랜잭션 사용 예시 </h3>

- "구매자가 판매자에게 금액송금" 을 대략적인 코드로 구현

<h4> 1) 트랜잭션 자체를 적용하지 않은 경우 </h4>

<h4> 2) @Transactional 대신 try-catch로 구현한 경우 </h4>

<h4> 3) @Transactional을 사용한 경우 </h4>

<h3> 1) 트랜잭션 자체를 적용하지 않은 경우 </h3>

```java

@Autowired
private Buyer buyer

@Autowired
private Seller seller;

public void buy() {

  buyer.send();			
  seller.receive();
      
}
```

- 이러한 경우 문제가 생길 수 있는 부분이 `receive()` 메소드 자체에 문제가 있어서 항상 `send()` 까지는 매번 실행이 되고 `receive()` 메소드는 실행이 되지 않을 경우
  - **구매자는 돈을 보내서 DB상에 금액이 줄어들었는데, 판매자는 입금이 되지 않아 DB상에 금액 변동이 없는 경우이다.**
-  반드시 transaction을 걸어서, **receive() 가 실행되지 못하고 에러가 난 경우 반드시 send() 또한 롤백되어 원상복구** 시켜주어야 한다.


<h3> 2) @Transactional 대신 try-catch로 구현한 경우 </h3>

```java

@Autowired
private PlatformTransactionManager transactionManager;

@Autowired
private Buyer buyer

@Autowired
private Seller seller;

public void buy() {

  DefaultTransactionDefinition def = new DefaultTransactionDefinition();
  TransactionStatus status = transactionManager.getTransaction(def);

  try {
      buyer.send();			
      seller.receive();
      
      transactionManager.commit(status);

  } catch(Exception e) {

      transactionManager.rollback(status);

  } 
}
```

- TransactionManager로 직접 커밋과 롤백을 시켜주었다.
  - 쿼리를 사용하는 메소드에 매번 중복되는 코드를 작성해 주어야 하는 불편함이 있다.

<h3> 3) @Transactional을 사용한 경우 </h3>

```java

@Autowired
private Buyer buyer

@Autowired
private Seller seller;

@Transactional
public void buy() {

  buyer.send();			
  seller.receive();
  
}

```

- 사용될 메서드 위에 @Transactional 어노테이션만 붙여주면, 위의 try-catch문을 작성하지 않아도 된다.

출처 : https://sky-h-kim.tistory.com/16 [[Spring] @Transactional 이란?]
