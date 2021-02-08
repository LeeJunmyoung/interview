# 3. DB

- [3. DB](#3-DB)
    - [Lock](#lock)
        - [Lock 이란](#lock-이란)
        - [Lcok 종류](#lock-종류)
            - [공유(Shared) Lock](#공유Shared-Lock)
            - [베타(Exclusive) Lock](#베타Exclusive-Lock)
        - [블로킹 (Blocking)](#블로킹-Blocking)
        - [교착상태 (Deadlock)](#교착상태-Deadlock)
- [참고](#참고)  

</br>

## Lock

### Lock 이란
> 트랜잭션 처리의 순차성을 보장하기 위한 방법.  
> 트랜잭션 처리능력이 핵심적인 요소.  
> 같은 자원을 액세스하려는 다중 트랜잭션 환경에서 데이터베이스의 일관성, 무결성 유지를 위해 트랜잭션의 순차적 진행을 보장하는 직렬화(serialization) 장치가 필요.  
> DBMS 마다 Lock 을 구현하는 세부 기능이 다름.  

### Lock 종류  

</br>

#### 공유(Shared) Lock
> 공유(Shared) Lock 은 데이터를 읽고자 할 때 사용된다.    
> 다른 공유 Lock 과는 호환되나, 배타적 Lock 과는 호환되지 않는다.    
> 자신이 읽고있는 리소스를 다른 사용자가 동시에 읽을 수 있어도, 변경은 불가하다.
> 다른 사용자가 읽고 있는 리소스를 동시에 읽을 수 있어도 변경 중인 리소스를 동시에 읽을 수 없다.
* 공유 Lock 을 설정한 리소스에 다른 트랜잭션이 추가로 Lock을 설정할 수 있으나, 배타적 Lock은 불가능하다. 

</br>

#### 베타(Exclusive) Lock
> 데이터를 변경하고자 할 때 사용되며, 트랜잭션이 완료될 때 까지 유지된다.  
> Lock이 해제될 때까지 다른 트랜잭션은 해당 리소스에 접근할 수 없다. 변경 불가, 읽기 불가.  
* 다른 트랜잭션에 의해 Lock 이 설정된 리소스는, 공유 Lock이든 배타적 Lock 이든 배타적 Lock 을 동시에 설정할 수 없다.

</br>

### 블로킹 (Blocking)
> Lock 경합이 발생해 특정 세션이 작업을 진행하지 못하고 멈춰 선 상태.  
> 공유 Lock 끼리는 호환되므로 블로킹 발생하지 않는다.  
> 공유 Lock , 배타적 Lock 은 호환되지 않아 블로킹 발생 할 수 있다. ( 배타적 Lock 끼리도 호환 안됨 )  
> 블로킹 상태 해소 방법은 커밋(또는 롤백).  
> 먼저 Lock 설정한 트랜잭션이 완료될 때 까지 후행 트랜잭션은 대기해야 하므로 성능 저하가 발생한다.  

</br>

### 교착상태 (Deadlock)
> 두 세션이 각각 Lock 을 설정한 리소스를 서로 액세스하려고 마주보며 진행하는 상황.    
> 교착상태가 발생하면 DBMS가 둘 중 한 세션에 에러를 발생시켜 문제를 해결한다.    
> 여러 테이블을 액세스하면서 발생하는 교착상태는 테이블 접근 순서를 같게 처리하면 피할 수 있다.  



</br>

#### 참고 
- http://wiki.gurubee.net/display/STUDY/1.Lock