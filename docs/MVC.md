## MVC

> **유지보수** 가 편해지는 코드 구성 방식

### MVC 패턴의 흐름
- 클라이언트는 필요한 기능을 컨트롤러에 요청한다.
- 컨트롤러는 알맞은 모델에게 비즈니스 수행 로직을 맡긴다.
- 알맞은 뷰를 선택한다.
- 결과 화면을 출력한다.

#### 예시
1. 사용자가 구글에 "코딩"이라고 검색한다. (사용자 -> Controller)
2. "코딩"에 대한 검색 결과 데이터를 달라고 요청한다. (Controller -> Model)
   - Model은 Controller에게 검색 결과 데이터를 반환한다.
3. Model한테 받은 검색 결과 데이터를 View로 전달한다. (Controller -> View)
4. 사용자가 보는 UI(레이아웃)에 검색 결과 데이터를 넣어서 웹 페이지로 보여준다. (View -> 사용자)

### Model
> 데이터와 비즈니스 로직과 관련된 부분을 담당한다.

- 데이터와 행동을 갖는 객체이다.
- 비즈니스 로직을 수행한다.
  - 상태 변화를 처리한다.
  - 상태 정보를 반환한다. 

### View
> 사용자에게 보여지는 부분을 담당한다.

- 데이터의 시각화이다.
- 모델이 처리한 데이터를 받아서 사용한다.
- 데이터와 로직이 포함되면 안 된다.

### Controller
> Model과 View를 이어주는 부분을 담당한다.

- 사용자의 요청을 해석하여 처리하고 결과를 반환하는 역할을 한다.
- 모델과 뷰를 느슨하게 연결한다.
- 데이터의 흐름을 제어한다.

### MVC를 지키면서 코딩하는 방법

#### 1. Model은 Controller와 View에 의존하지 않아야 한다. 
>Model 내부에 Controller와 View에 관련된 코드가 있으면 안 된다.

Model은 데이터와 관련된 부분이기 때문에, 언제든지 깔끔하고 정제된 데이터를 꺼내어 쓸 수 있도록
View나 Controller의 코드를 섞어서 사용하지 않고 데이터에 관련된 코드만 모아놓고자 했다.

```java
public class Student {
    private String name;
    private int age;
    
    public Student(String name , int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return name;
    }
    
    public String getAge() {
        return age;
    }
}
```

#### 2. View는 Model에만 의존해야 하고, Controller에는 의존하면 안 된다.
>View 내부에 Model의 코드만 있을 수 있고, Controller의 코드는 있으면 안 된다.

```java
public class OutputView {
    public void printProfile(Student student) {
        System.out.println(
                "내 이름은 " + student.getName() + "입니다.");
        System.out.println(
                "내 나이는 " + studnet.getAge() + "입니다.");
    }
}
```

#### 3. View가 Model로부터 데이터를 받을 때는, 사용자마다 다르게 보여주어야 하는 데이터에 대해서만 받아야 한다.
> 사용자에 상관 없이 공통적으로 보여지는 부분은 Model로부터 받는 것이 아닌, View가 자체적으로 가지고 있어야 하는 정보들이다. ex) 주문하기, 배달정보 텍스트

#### 4. Controller는 Model과 View에 의존해도 된다.
> Controller 내부에는 Model과 View의 코드가 있을 수 있다.

컨트롤러는 Model과 View의 중개자 역할을 하면서 전체 로직을 구성한다.

```java
public class Controller {
    public static void main(Stirng[] args) {
        Student student = new Student("기철", 25);
        OutputView.printProfile(Student);
    }
}
```

#### 5. View가 Model로부터 데이터를 받을 때, 반드시 Controller에서 받아야 한다.

<hr>

## Layer (5-layer)

### Service Logic
- 클래스 간의 관계를 관리한다.
- 상태를 저장한다.
- 트랜잭션을 가진다.
- Control-Persistance 계층을 연결한다.

### Domain Object
- 데이터와 행위를 갖는 객체이다.
- 핵심 비즈니스 로직이다.
- 주요 검증이 일어난다.
- Persistance Layer에 맵핑된다.

### Persistance Layer
- 데이터 처리(CRUD)를 담당한다.
- 주요 패턴 - DAO 패턴, ORM

<hr>

## 유효성 검증

### View
- 간단한 검증
  - 비어있는 값
  - 적절하지 않은 타입

### Controller
- 파라미터 존재 유무 검증

### Model
- 데이터 검증
- 로직에 대한 검증

#### 참고 자료
- [링크1 | MVC 테코톡](https://www.youtube.com/watch?v=ogaXW6KPc8I)
- [링크2 | MVC 테코톡](https://www.youtube.com/watch?v=es1ckjHOzTI)
- [링크3 | MVC 테코톡](https://www.youtube.com/watch?v=Yzx-z6kCD2A)
- [링크4 | MVC 테코톡](https://www.youtube.com/watch?v=86NxhHptx7s)