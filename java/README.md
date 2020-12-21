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
Queue|LinkedList</br>PriorityQueue|List와 유사
Map|HashTable</br>HashMap</br>TreeMap|키(key), 값(value)의 쌍으로 이루어진 데이터 집합.</br>순서는 유지되지 않으나 key의 중복을 허용하지 않으나 value의 중복은 허용  
* LinkedHashMap, LinkedHashSet의 경우 순서를 보장합니다.

#### List 종류 특징
- Vector : ArrayList와 유사하나 항상 동기화함. 싱글 스레드일 경우에도 동기화 하기때문
- ArrayList : index와 value를 같는 선형리스트. Random Access시 index값이 있기에 LinkedList보다 유리함.
- LinkedList :  각 노드가 데이터와 포인터를 가지고 한 줄로 연결되어 있는 방식의 자료구조, 추가 / 삭제시 포인터만 변경하면 되기에 ArrayList보다 유리함.

#### Set 종류 특징
- HashSet : HashSet은 순서의 정렬을 가지지 않고, 컬렉션의 객체 저장을 목적으로하는 일반적인 Set
- TreeSet : '레드-블랙 트리(Red-Black Tree)로 구현되어 있음. 데이터의 추가, 삭제에는 시간이 걸리지만, 검색과 정렬이 뛰어나다는 장점
LinkedHashSet : 들어오는 데이터의 순서를 보장 Set

#### Queue 종류 특징
- PriorityQueue : 먼저 들어온 순서대로 데이터가 나가는 것이 아닌 우선순위를 먼저 결정하고 그 우선순위가 높은 엘리먼트가 먼저 나가는 자료구조  
- LinkedList : FIFO(First-In-First-Out) 구조의 자료구조

</br>

#### 참고
- https://www.javatpoint.com/collections-in-java