# Java 컬렉션 프레임워크

## List 인터페이스

### ArrayList
- 인덱스로 접근할 때는 ArrayList를 사용하는 것이 좋다.

#### 장점 (배열과 비교했을 때)
- 다양한 기능을 제공 받기 때문에 편하다.
- 배열은 함께 변하지만, 제네릭은 함께 변하지 않기 때문에 타입 안정성을 보장한다. (컴파일 예외가 발생한다.)

### LinkedList
- 요소를 삽입, 삭제할 때는 LinkedList를 사용하는 것이 좋다.
- 하지만 비순차적인 삽입, 삭제의 경우에는 불리하다.

## legacy 클래스

## Vector
- 배열 기반이며 동기화 된다. 
- 모든 메서드에 synchronized 키워드가 있다.
- 한 스레드가 해당 메서드를 실행하면 다른 스레드들은 접근할 수 없다.

## Stack
- vector를 상속 받는다.
- LIFO가 지켜지지 못할 수 있다.

## Queue 인터페이스

### ArrayDeque
- ArrayDeque는 Resizable 배열로 구현된다.
- 스레드 세이프하지 않다.
- LinkedList와 달리 Null 요소를 허용하지 않는다.
- 배열이지만 삽입 삭제가 constant time이다.
- O(1)의 시간 복잡도를 가진다.

## Map 인터페이스

### HashMap
- 각각의 Key 값이 해시 함수에 의해 고유한 인덱스를 가지게 되어 값에 바로 접근할 수 있다.
- 순서는 보장되지 않는다.
- 평균 O(1)의 시간 복잡도로 데이터를 조회한다.
- 입력된 순서를 보장하려면 LinkedHashMap을 사용하면 된다.

### TreeMap
- 정렬된 상태로 데이터를 조회하거나
- 범위를 검색할 때 좋다.

#### 참고 자료

[링크1 | 컬렉션 프레임워크 테코톡](https://www.youtube.com/watch?v=FrPCDEiindY)