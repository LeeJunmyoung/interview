# 2. Spring

- [2. Spring](#2-spring)
    - [@Transactional](#transactional)
        - [@Transactional 옵션](#transactional-옵션)
            - [isolation](#isolation)
            - [propagation](#propagation)
        - [@Transactional 사용 예시](#transactional-사용-예시)
- [참고](#참고)  
    -[참고-transactional](#참고-transactional)  

</br>


## @Transactional
> 클래스나, 메소드에 대한 트랜잭션을 설정한다.

</br>
 
### @Transactional 옵션

구분 | 내용
---|---
isolation|트랜잭션에서 일관성 허용 수준을 설정
propagation|트랜잭션 동작 도중 다른 트랜잭션을 호출할 때, 어떻게 할 것인지 지정하는 옵션
noRollbackFor|특정 예외 발생 시 rollback하지 않음 지정  
rollbackFor|특정 예외 발생 시 rollback함.
timeout|지정한 시간 내에 메소드 수행이 완료되지 않으면 rollback 함  (-1일 경우 timeout을 사용하지 않음)
readOnly | 트랜잭션을 읽기 전용으로 설정

</br>

### isolation
> 트랜잭션에서 일관성 허용 수준을 설정  
> ACID 의 I에 해당.  
> 독립성(Isolation)은 트랜잭션을 수행 시 다른 트랜잭션의 연산 작업이 끼어들지 못하도록 보장하는 것을 의미한다.  
> 이것은 트랜잭션 밖에 있는 어떤 연산도 중간 단계의 데이터를 볼 수 없음을 의미한다.  
> 은행 관리자는 이체 작업을 하는 도중에 쿼리를 실행하더라도 특정 계좌간 이체하는 양 쪽을 볼 수 없다.  
> 공식적으로 고립성은 트랜잭션 실행내역은 연속적이어야 함을 의미한다.  
> 성능관련 이유로 인해 이 특성은 가장 유연성 있는 제약 조건이다. 

</br>

구분 | 내용
---|---
DEFAULT | - DB의 isolation 정책을 따름
READ_UNCOMMITTED | - 아직 Commit되지 않은 트랜잭션에 의해 변경된 데이터를 읽어 올수 있다. <br><br> - X라는 트랜잭션이 A데이터가 B로 커밋되지 않아도 Y트랜잭션에서는 B라고 읽어온다. (Dirty read) <br><br> - X트랜잭션이 롤백되면 Y트랜잭션은 잘못된 행을 검색하게 된다. <br><br> - Dirty read : 아직 완료되지 않은 트랜잭션을 다른 트랜잭션에서 읽어올수 있는 것을 dirty read라 한다.<br> READ UNCOMMITTED 격리수준에서만 일어나는 현상
READ_COMMITTED | - 트랜잭션이 커밋되지 않은 변경 사항이있는 행을 읽는 것을 금지  <br><br> - dirty read 방지  <br><br> - X라는 트랜잭션이 commit 되기 전 까지는 다른 트랜잭션에서는 변경된 데이터를 검색할 수 없다. <br><br> - 단, X라는 트랜잭션과 Y라는 트랙잰션에서 X라는 데이터 A가 B로 변경되어 커밋시 <br> Y는 X가 커밋전에는 A로 커밋 후에는 B로 보이는 Non-Repeatable Read가 발생함. 
REPEATABLE_READ | - Transaction이 범위내에서는 조회한 데이터의 내용이 항상 동일함을 보장해 줌.  <br><br> - Non-Repeatable Read 방지  <br><br> - SELECT시 현재 시점의 스냅샷을 만들고 스냅샷을 조회함.  <br><br> - 단, 다른 트랜잭션에서 Where절에 포함하는 새로운 레코드가 insert되면 유령(phantom) 레코드가 보이게 된다.  
SERIALIZABLE | - 완벽한 읽기 일관성 모드 제공(가장 엄격함)  <br><br> - Phantom Read 방지 <br><br> - 성능 측면에서 동시 처리성능이 가장 낮다. <br><br> - 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 shared lock이 걸리므로<br> 다른 사용자는 그 영역에 해당하는 데이터에 대한 수정 및 입력이 불가능  

<br>

### propagation
> 트랜잭션 동작 도중 다른 트랜잭션을 호출할 때, 어떻게 할 것인지 지정하는 옵션  
> 사용할 트랜잭션 전파 동작을 선언할수 있음.  

<br>

구분 | 내용
---|---
REQUIRED | - 기본속성<br> - 이미 트랜잭션이 있으면 참여하고 없으면 새로 시작
REQUIRED_NEW | - 기존 트랜잭션과는 별개로 새로운 트랜잭션을 시작함.<br> - 기존 트랜잭션은 보류
MANDATORY | - 트랜잭션이 있으면 참여하고, 없으면 예외 발생.  
SUPPORTS | 트랜잭셔이 있으면 참여하고, 없으면 트랜잭션 없이 진행.   
NOT_SUPPPORTED | 트랜잭션을 사용하지 않음.<br> - 이미 진행중인 트랜잭션이 있다면 보류함.  
NEVER | - 트랜잭션을 사용하지 않음. <br> - 이미 트랜잭션이 존재한다면 예외 발생  
NESTED | - 이미 진행중인 트랜잭션이 있다면 중첩 트랜잭션을 시작함 <br> - REQUIRED_NEW와 차이는 부모의 트랜잭션에 따라 영향을 받음 <br> - 본인은 부모에게 영향을 주지 않음.


</br>

### @Transactional 사용 예시
```
아래와 같이 플로우가 되어 있었는데
승인후작업시 DB lock(대게)이나 사람 실수 등으로 간혹
Exception이 발생함. 하지만 API요청한 데이터 로그는 DB에 적재해야하는 일이 생김
그래서 API요청데이터적재에 REQUIRED_NEW로 설정하여 문제 해결.

만약 승인 후 작업시 예외가 발생해서 적재된 로그도 지워야한다면 NESTED 로 했을거임 
그럼 로그 적재시 예외발생할때는 부모 트랜잭션에는 영향이 없을 테니깐. 

// REQUIRED 
public 결제프로세스() throws Exception() {

    유호성검증()

    주문프로세스()

    PG사승인요청()

    승인후작업()
}

public PG사승인요청() {
    PG사_API요청()

    API요청데이터로그적재()
}
```

#### 참고 

##### 참고-transactional
- https://taetaetae.github.io/2016/10/08/20161008/ 
- https://nesoy.github.io/articles/2019-05/Database-Transaction-isolation
- http://wiki.gurubee.net/pages/viewpage.action?pageId=21200923
- https://medium.com/@wonderful.dev/isolation-level-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-94e2c30cd8c9
- https://bamdule.tistory.com/51