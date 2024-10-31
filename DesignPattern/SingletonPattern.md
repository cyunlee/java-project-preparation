# 싱글턴 패턴과 정적 클래스

프로그램 전역에서 이용되는 **유일한 클래스**를 만드는 방법
- 싱글턴 패턴 이용하기
- 정적 클래스 이용하기

## 싱글턴 패턴이란?
> 객체의 인스턴스가 오로지 한 개만 생성되도록 설계하는 패턴
> - When? : 로그 기록, 캐싱, 사용자 설정 등에서 사용된다.
> - Why? : 유일성, 글로벌

## 싱글턴 패턴 실습

ex) Settings : 배경색을 담당하는 클래스가 애플리케이션 내부에서 유일하지 않다면?

### 1. 순수한 구현
> 문제점 : 멀티 스레드 환경에서 안전하지 않다.

- 인스턴스를 private static 변수
- getInstance()에서 인스턴스 생성
- 외부 생성자를 막는다

```java
public class Settings {
    private static Settings instance;
    
    private Settings() {
        
    }
    
    public static Settings getInstance() {
        if (instance==null) {
            instance = new Settings();
        }
        return instance;
    }
}

public class App {
    public static void main(String[] args) {
        Settings settings1 = Settings.getInstance();
        Settings settings2 = Settings.getInstance();

        System.out.println(settings1);
        System.out.println(settings2);
        System.out.println(settings1 == settings2);
    }
}
```

### 2. 동기화(Synchronized)
> 문제점 : 리소스가 낭비된다. (But, 동시성의 문제를 해결할 수 있다.)

- 인스턴스를 private static 변수
- synchronized getInstance()
- 외부 생성자를 막는다.

### 3. Double Checked Locking(DCL)
> 문제점 : JVM에 따라 스레드 세이프x (사용하지 말자)

- synchronized 시점 지연
- private static volatile 인스턴스
- 외부 생성자를 막는다.

```java
public class Settings {
    private static volatile Settings instance;
    
    private Settings() {
        
    }
    
    public static Settings getInstance() {
        if (instance == null) {
            synchronized (Settings.class) {
                if (instance == null) {
                    instance = new Settings();
                }
            }
        }
        return instance;
    }
}
```

### 4. Bill Pugh Solution ★
> 문제점 : 리플레션, 직렬화

- static inner class 인스턴스
- 생성자를 private

```java
public class Settings {
    private Settings() {
        
    }
    
    private static class SettingsHolder {
        private static final Settings SETTINGS = new Settings();
    }
    
    public static Settings getInstance() {
        return SettingsHolder.SETTINGS;
    }
}
```

### Enum ★
> 문제점 : 싱글턴 해제 번거로움, Enum외의 클래스 상속 불가능

- instance

```java
public enum Settings {
    INSTANCE;
}
```

## 정적 클래스와의 차이점

### 정적 클래스
> 정적 메서드만 갖고 있는 클래스

## 싱글턴과 정적 클래스를 언제 사용할까?

### 싱글턴 패턴
- 상속 받아서 사용 가능하다.
- 메서드 파라미터로 사용 가능하다.
- 권장 환경
    - 완벽한 객체지향을 필요로 할 때
    - 레이지 로딩이 필요할 때

### 정적 클래스
- 객체 생성을 하지 않는다.(효율성)
- 권장 환경
    - 유틸 메서드를 보관하는 용도로 사용할 때
    - 다형성이나 상속이 필요없는 클래스

#### 참고 자료
[링크1|싱글턴 패턴 테코톡](https://www.youtube.com/watch?v=5oUdqn7WeP0)