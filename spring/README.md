# 2. Spring

- [2. Spring](#2.-Spring)
    - [@Transactional](#@Transactional)
        - [@Transactional 속성](#@Transactional-속성)
            - [isolation](#isolation)
                - [DEFAULT](#DEFAULT)
                - [READ_UNCOMMITTED](#READ_UNCOMMITTED)
                - [READ_COMMITTED](#READ_COMMITTED)
                - [REPEATABLE_READ](#REPEATABLE_READ)
                - [SERIALIZABLE](#SERIALIZABLE)
            - [propagation](#propagation)
- [참고](#참고)  
    -[참고-isolation](#참고-isolation)  

</br>


## @Transactional
> 클래스나, 메소드에 대한 트랜잭션을 설정한다.

</br>
 
### @Transactional 속성

</br>

### isolation
> ACID 의 I에 해당.  
> 독립성(Isolation)은 트랜잭션을 수행 시 다른 트랜잭션의 연산 작업이 끼어들지 못하도록 보장하는 것을 의미한다.  
> 이것은 트랜잭션 밖에 있는 어떤 연산도 중간 단계의 데이터를 볼 수 없음을 의미한다.  
> 은행 관리자는 이체 작업을 하는 도중에 쿼리를 실행하더라도 특정 계좌간 이체하는 양 쪽을 볼 수 없다.  
> 공식적으로 고립성은 트랜잭션 실행내역은 연속적이어야 함을 의미한다.  
> 성능관련 이유로 인해 이 특성은 가장 유연성 있는 제약 조건이다. 

</br>

구분 | 내용
---|---
Default | - DB의 isolation 정책을 따름
READ_UNCOMMITTED | - 아직 Commit되지 않은 트랜잭션에 의해 변경된 데이터를 읽어 올수 있다. <br><br> - X라는 트랜잭션이 A데이터가 B로 커밋되지 않아도 Y트랜잭션에서는 B라고 읽어온다. (Dirty read) <br><br> - X트랜잭션이 롤백되면 Y트랜잭션은 잘못된 행을 검색하게 된다. <br><br> - Dirty read : 아직 완료되지 않은 트랜잭션을 다른 트랜잭션에서 읽어올수 있는 것을 dirty read라 한다.<br> READ UNCOMMITTED 격리수준에서만 일어나는 현상
READ_COMMITTED | - 트랜잭션이 커밋되지 않은 변경 사항이있는 행을 읽는 것을 금지  <br><br> - dirty read 방지  <br><br> - X라는 트랜잭션이 commit 되기 전 까지는 다른 트랜잭션에서는 변경된 데이터를 검색할 수 없다. <br><br> - 단, X라는 트랜잭션과 Y라는 트랙잰션에서 X라는 데이터 A가 B로 변경되어 커밋시 <br> Y는 X가 커밋전에는 A로 커밋 후에는 B로 보이는 Non-Repeatable Read가 발생함. 
REPEATABLE_READ | - Transaction이 범위내에서는 조회한 데이터의 내용이 항상 동일함을 보장해 줌.  <br><br> - Non-Repeatable Read 방지  <br><br> - SELECT시 현재 시점의 스냅샷을 만들고 스냅샷을 조회함.  <br><br> - 단, 다른 트랜잭션에서 Where절에 포함하는 새로운 레코드가 insert되면 유령(phantom) 레코드가 보이게 된다.  
SERIALIZABLE | - 완벽한 읽기 일관성 모드 제공(가장 엄격함)  <br><br> - Phantom Read 방지 <br><br> - 성능 측면에서 동시 처리성능이 가장 낮다. <br><br> - 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 shared lock이 걸리므로<br> 다른 사용자는 그 영역에 해당하는 데이터에 대한 수정 및 입력이 불가능  


### propagation
> 트랜잭션 동작 도중 다른 트랜잭션을 호출(실행)하는 상황이에 선택할 수 있는 옵션  
> 사용할 트랜잭션 전파 동작을 선언할수 있음.  


</br>

#### 참고 

##### 참고-isolation 
- https://taetaetae.github.io/2016/10/08/20161008/ 
- https://nesoy.github.io/articles/2019-05/Database-Transaction-isolation
- http://wiki.gurubee.net/pages/viewpage.action?pageId=21200923
- https://medium.com/@wonderful.dev/isolation-level-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-94e2c30cd8c9