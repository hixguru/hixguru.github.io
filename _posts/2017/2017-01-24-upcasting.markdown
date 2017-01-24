---
layout: "post"
title: "Upcasting"
date: "2017-01-24 23:13"
---

### 업캐스팅
> 업캐스팅(Upcasting)이란 하위 클래스형이 상위 클래스형으로 캐스팅 되는 것.

#### 기본 데이터 타입(Primitive Data type)의 캐스팅

- 일반적인 캐스팅은 작은 데이터 타입이 큰 데이터 타입으로 캐스팅 되는 것이다.

  - 작은 > 큰 : 일반적인 형태
```java
byte b = 127;
int i = b;
```
  - 큰 > 작은 : 데이터 손실, 오버플로우 발생 가능성
```java
int i = 128;
byte b = (byte) i;
```

- 클래스의 경우 하위 클래스형(큰)에서 상위 클래스형(작은)으로 캐스팅이 가능하다.

```java
class ShapeMain {
  public static void main(String... args) {
    Shape shape = new Shape();
    shape.draw(); // 그려, 그냥 막 그려

    Circle circle = new Circle();
    circle.draw();

    // 업캐스팅이 됐을 경우, casting은 Circle class 메모리 영역에 접근할 수 없지만,
    // 오버라이딩된 메소드가 있다면 가상 메소드 기법을 이용하여 재정의된 메소드를 호출한다.
    Shape casting = new Circle();
    casting.draw(); // 원 그냥 그려
  }
}

class Circle extends Shape {
  private String type = "원";

  @Override public void draw() {
    System.out.println(type + " 그냥 그려");
  }
}

class Shape {
  public void draw() {
    System.out.println("그려, 그냥 막 그려");
  }
}
```


- 추상 클래스의 업캐스팅

```java
public class Vayne extends Champions {

  public static void main(String... args) {
    // 추상클래스 형태임에도 불구하고 객체를 생성하고 추상 메소드를 실행할 수 있는 이유는 업캐스팅이 이루어졌기 때문
    // 해당 추상메소드가 오버라이딩 됐는지 확인하고, 됐다면 하위 클래스가 재정의한 메소드를 실행시킨다.
    Champions vayne = new Vayne();
    vayne.voice();
  }

  @Override void voice() {
    System.out.println("이 사건은 제가 맡죠.");
  }
}

/**
 * 추상클래스는 불완전한 클래스로 추상메소드가 구현되지 않았을 뿐더러 객체를 생성할 수 없다.
 * 그러나 추상클래스도 클래스의 역할(상위 클래스로서의 업캐스팅)은 할 수 있다.
 */
abstract class Champions {
  abstract void voice();
}
```


- 인터페이스의 업캐스팅

```java
public class TeamFight {
  public static void main(String... args) {
    // 인터페이스도 하나의 클래스 역할로 업캐스팅이 가능하지만,
    // 상위 클래스에서 있으며 하위 클래스에서 구현된 가상메소드만 사용이 가능하다.
    TopLaner topLaner = new Role();
    topLaner.tanking();

    JungleLaner jungleLaner = new Role();
    jungleLaner.ganking();

    MidLaner midLaner = new Role();
    midLaner.nuking();

    BottomLaner bottomLaner = new Role();
    bottomLaner.farming();
  }
}

class Role implements TopLaner, MidLaner, JungleLaner, BottomLaner {

  @Override public void tanking() {
    System.out.println("탑차이 15g네");
  }

  @Override public void nuking() {
    System.out.println("미드 딜 실화냐");
  }

  @Override public void ganking() {
    System.out.println("우리 정글은 rpg하러옴?");
  }

  @Override public void farming() {
    System.out.println("바텀은 게임 터지는데 cs만 먹네");
  }
}



/**
 * 인터페이스도 추상클래스와 마찬가지로 구현체가 없어 불완전하지만 `클래스`로서의 업캐스팅이 가능하다.
 */
interface TopLaner {
  void tanking();
}

interface MidLaner {
  void nuking();
}

interface JungleLaner {
  void ganking();
}

interface BottomLaner {
  void farming();
}
```

#### 결과
![interface](../../../assets/images/upcasting.png)


예제가 다소 리그 오브 레전드 위주이긴 하지만, 공부 또한 ~자기가 관심있는 분야에 접목시키면 더 잘 되는 연구가 있다~는 믿음과 함께 예제를 작성해보았다. 자바를 복습하면서 하나둘 안드로이드 유명 라이브러리를 적용시켰을 때 이해가 되지 않던 조각조각들이 하나의 퍼즐로 연결되는 느낌을 받는다. 아직도 공부할 내용들이 많지만 조급하지 않게 천천히 공부해보자.
