# 1. JAVA

- [1. JAVA](#1.-JAVA)
    - [Collection](#Collection)
        - [배열과의 차이점](#배열과의-차이점)
        - [컬렉션 프에임 워크 계층구조](#컬렉션-프에임-워크-계층구조)
            - [Collection 계층구조](#Collection-계층구조)
            - [Map 계층구조](#Map-계층구조)
        - [특징](#특징)
            - [List](#List-종류-특징)
            - [Set](#Set-종류-특징)
            - [Queue](#Queue-종류-특징)
            - [Map](#Map-종류-특징)
        - [동기화, 병렬 컬렉션](#동기화,-병렬-컬렉션)
            - [동기화된(synchronized) 컬렉션](#동기화된(synchronized)-컬렉션)
            - [병렬(concurrent) 컬렉션](#병렬(concurrent)-컬렉션)
- [참고](#참고)
</br>

## Collection
> 자바에서 컬렉션 프레임워크(collection framework)란 다수의 데이터를 쉽고 효과적으로 처리할 수 있는 표준화된 방법을 제공하는 클래스의 집합  
> 데이터를 저장하는 자료 구조와 데이터를 처리하는 알고리즘을 구조화하여 클래스로 구현해 놓은 것

</br>

### 배열과의 차이점
> 컬렉션과 배열은 둘 다 개체에 대한 참조를 보유하고 그룹으로 관리 할 수 ​​있다는 점에서 유사  
> 그러나 어레이와 달리 컬렉션은 인스턴스화 할 때 특정 용량을 할당 할 필요가 없음  
> 컬렉션은 개체를 추가하거나 제거 할 때 자동으로 크기를 늘리거나 줄일 수 있음  
> 컬렉션은 int, long 또는 double과 같은 기본 데이터 유형 요소 (기본 유형)를 지정 할 수 없으나 Integer, Long 또는 Double과 같은 래퍼 클래스로 지정 가능  

</br>

### 컬렉션 프레임 워크 계층 구조  

#### Collection
![ ](img/java-collection-hierarchy.png)

#### Map
![ ](img/java-map-hierarchy.png)

</br>

### 특징  
인터페이스 | 구현클레스 | 특징  
:---:|:---:|:---  
Set|HashSet</br>TreeSet|순서를 유지하지 않는 데이터의 집합으로 데이터의 중복을 허용하지 않음
List|LinkedList</br>Vector</br>ArrayList|순서가 있는 데이터의 집합으로 데이터의 중복을 허용  
Queue|LinkedList</br>PriorityQueue|FIFO (First In First Out) 방식으로 요소를 정렬</br>PriorityQueue 클래스는 큐 사용 기능을 제공합니다. 그러나 FIFO 방식으로 요소를 정렬하지 않음
Map|HashTable</br>HashMap</br>TreeMap|키(key), 값(value)의 쌍으로 이루어진 데이터 집합.</br>순서는 유지되지 않으나 key의 중복을 허용하지 않으나 value의 중복은 허용  
* LinkedHashMap, LinkedHashSet의 경우 순서를 보장합니다.
* Stack의 경우 Vector(항상 동기화)를 상속받기 때문에 잘 사용안함.

</br>

#### List 종류 특징
- Vector : ArrayList와 유사하나 항상 동기화함. 싱글 스레드일 경우에도 동기화 함.
- ArrayList : index와 value를 같는 선형리스트. Random Access시 index값이 있기에 LinkedList보다 유리함.
- LinkedList :  각 노드가 데이터와 포인터를 가지고 한 줄로 연결되어 있는 방식의 자료구조, 추가 / 삭제시 포인터만 변경하면 되기에 ArrayList보다 유리함.

</br>

#### Set 종류 특징
- HashSet : HashSet은 순서의 정렬을 가지지 않고, 컬렉션의 객체 저장을 목적으로하는 일반적인 Set
- TreeSet : '레드-블랙 트리(Red-Black Tree)로 구현되어 있음. 데이터의 추가, 삭제에는 시간이 걸리지만, 검색과 정렬이 뛰어나다는 장점
LinkedHashSet : 들어오는 데이터의 순서를 보장하는 Set

</br>

#### Queue 종류 특징
- PriorityQueue : 먼저 들어온 순서대로 데이터가 나가는 것이 아닌 우선순위를 먼저 결정하고 그 우선순위가 높은 엘리먼트가 먼저 나가는 자료구조  
- LinkedList : FIFO(First-In-First-Out) 구조의 자료구조  


</br>

#### Map 종류 특징
- HashMap : Map의 특징인 key와 value의 쌍으로 이루어지며, key 또는 value 값으로써 null을 허용   
- HashTable : HashMap과 유사하나 항상 동기화함. key 또는 value값으로 null을 허용하지 않음.  
- LinkedHashMap : 들어오는 데이터의 순서를 보장하는 Map  
- TreeMap : '레드-블랙 트리(Red-Black Tree)로 구현되어 있음. 데이터의 추가, 삭제에는 시간이 걸리지만, 검색과 정렬이 뛰어나다는 장점. Key(null을 허용하지 않음)값을 기준으로 정렬 됨.  

</br>

### 동기화, 병렬 컬렉션

#### 동기화된(synchronized) 컬렉션
> - Vector, Hashtable, Collections.synchronizedXXX()로 생성된 컬렉션들  
> 문제점: Thread Safe하나, 두개 이상의 연산을 묶어서 처리해야 할 때 외부에서 동기화 처리를 해줘야 한다. (Iteration, put-if-absent, replace, condition-remove 등)  
> Since JDK 1.2  

#### 병렬(concurrent) 컬렉션
> List: CopyOnWriteArrayList  
> Map: ConcurrentMap, ConcurrentHashMap  
> Set: CopyOnWriteArraySet  
> SortedMap: ConcurrentSkipListMap (Since Java 6)  
> SortedSet: ConcurrentSkipListSet (Since Java 6)  
> Queue 계열:ConcurrentLinkedQueue  
> 특이사항: Concurrent(병렬/동시성)이란 단어에서 알 수 있듯이 Synchronized 컬렉션과 달리 여러 스레드가 동시에 컬렉션에 접근할 수 있다. ConcurrentHashMap의 경우, lock striping 이라 부르는 세밀한 동기화 기법을 사용하기 때문에 가능하다. 구현 소스를 보면 16개의 락 객체를 배열로 두고 전체 Hash 범위를 1/16로 나누어 락을 담당한다. 최대 16개의 스레드가 경쟁없이 동시에 맵 데이터를 사용할 수 있음  
> 반대로 단점도 있는데, clear()와 같이 전체 데이터를 독점적으로 사용해야할 경우, 단일 락을 사용할 때보다 동기화 시키기도 어렵고 자원도 많이 소모하게 된다. 또한, size(), isEmpty()같은 연산이 최신값을 반환하지 못할 수도 있다. 하지만 내부 상태를 정확하게 알려주지 못한다는 단점이 그다지 문제되는 경우는 거의 없다.  
> Since Java 5,6

#### 참고, 출처
- https://www.javatpoint.com/collections-in-java
- https://deepblue28.tistory.com/entry/Java-SynchronizedCollections-vs-ConcurrentCollections (동기화, 병렬 컬렉션)