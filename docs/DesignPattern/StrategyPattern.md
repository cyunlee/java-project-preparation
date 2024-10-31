# 전략 패턴 Strategy Pattern

## 전략이란?
> 특정한 목표를 수행하기 위한 행동 계획

ex) 배민 로봇 전략 예시
- 이동 전략 Move Strategy
  - Walk 걸어서
  - Run 뛰어서
  - Fly 날아서
  - Rocket 로켓으로
- 온도 전략 Temp Strategy
  - Cold 차갑게
  - Warm 따뜻하게
  - Frozen 냉동으로
  - Hot 뜨겁게

## 전략 패턴이란?
> 객체가 할 수 있는 **행위**들 각각을 **전략**으로 만들어 놓고 사용하며, 동적으로 **전략 수정**이 가능한 패턴

## 전략 패턴의 의도
> - 전략을 분리해야 한다.
> - 상호 교환의 기능을 추가할 수 있다. (setter를 이용한다.)

- 동일 계열의 알고리즘 군을 정의하고 ex) walk, run, fly, rocket
- 각 알고리즘을 캡슐화하며 ex) Move Strategy
- 이들을 **상호교환**이 가능하도록 만든다.

```java
public class Main {
  public static void main(String[] args) {
    Robot robot = new Robot(new Walk(), new Cold());
    
    robot.move();
    robot.temperature();
  }
}

public class Robot {
  private MoveStrategy moveStrategy;
  private TemperatureStrategy temperatureStrategy;

  public Robot(MoveStrategy moveStrategy, TemperatureStrategy temperatureStrategy) {
    this.moveStrategy = moveStrategy;
    this.temperatureStrategy = temperatureStrategy;
  }

  public void move() {
    moveStrategy.move();
  }

  public void temperature() {
    temperatureStrategy.temperature();
  }
}

public interface MoveStrategy {
  void move();
}

public class Walk implements MoveStrategy {
  @Override
  public void move() {
    System.out.println("걸어서 배달합니다.");
  }
}

public class Run implements MoveStrategy {
  @Override
  public void move() {
    System.out.println("뛰어서 배달합니다.");
  }
}

public interface TemperatureStrategy {
  void temperature();
}

public class Cold implements TemperatureStrategy {
  @Override
  public void temperature() {
    System.out.println("차갑습니다.");
  }
}

public class Warm implements TemperatureStrategy {
  @Override
  public void temperature() {
    System.out.println("따뜻합니다.");
  }
}
```

#### 참고 자료

[링크1 | 전략패턴 테코톡](https://www.youtube.com/watch?v=vNsZXC3VgUA)