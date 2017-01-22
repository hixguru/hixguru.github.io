---
layout: "post"
title: "추상(abstract) 클래스와 인터페이스(interface)"
date: "2017-01-22 22:59"
---

오늘은 비슷하지만 다른 모습을 가진 Java에서의 추상 클래스(Abstract Class)와 인터페이스(Interface)의 차이에 대해서 알아보고자 한다. 기본적인 내용이지만 한번은 다시금 상기해볼 만한 Java에서의 핵심적인 기능이다. 추상 클래스와 인터페이스에 대해서 공부하다 보니, MVP + Dagger2를 사용할 때 반환형을 인터페이스로 명시하고 해당 인터페이스를 implements한 클래스의 인스턴스를 넘기는지 이제 이해가 됐다. 주절주절 주저리는 이쯤으로 해두고 코드를 통해 함께 알아보자 :D

## 추상 클래스(Abstract Class)

```java
/**
 * Created by hwanik on 2017. 1. 22..
 */
public class ExtendsClass extends AbstractClass {

    /**
     * @Override 어노테이션은 굳이 명시하지 않아도 된다.
     * 추상 클래스의 추상 메소드를 전부 구현해야만 온전한 객체를 생성할 수 있다.
     * 추상 메소드를 모두 구현하지 않을 경우 상속받은 클래스도 추상클래스가 되어 객체를 만들어 사용할 수 없다.
     */
    @Override //
    public void sayHelloWorld() {
        System.out.println("say Hello World");
    }

    public static void main(String... args) {
        ExtendsClass test = new ExtendsClass();
        test.sayHelloWorld();
    }
}

/**
 * 추상: 완전하지 않은, 불완전한, 객체를 생성할 수 없는 class
 * 추상 클래스는 추상 메소드를 가진 클래스를 말하며 class앞에 abstract를 꼭 명시해줘야 한다.
 * 추상 메소드를 가지고 있지 않더라도, 추상 클래스로 명시하여 `상속` 전용으로 사용할 수도 있다.
 * 인터페이스(interface)와 다르게 일반 메소드와 추상 메소드를 동시에 가질 수 있으며 extends로 상속받아 구현된다.
 */
abstract class AbstractClass {
    public void sayHello() {
        System.out.println("say Hello");
    }

    public void sayHi() {
        System.out.println("say Hi");
    }

    // 추상 메소드는 메소드의 `프로토 타입`(구현되지 않은)만 가지고 있다라고 한다.
    public abstract void sayHelloWorld();
}
```

## 인터페이스(Interface)

```java
/**
 * Created by hwanik on 2017. 1. 22..
 */
public class Katelyn implements Champion {

    public static void main(String... args) {
        Katelyn katelyn = new Katelyn();
        katelyn.useSkill(Champion.SKILL_Q);
        katelyn.useSkill(Champion.SKILL_W);
        katelyn.useSkill(Champion.SKILL_E);
        katelyn.useSkill(Champion.SKILL_R);
    }

    // 추상 메소드를 모두 구현해야한다. 모두 구현하지 않을 경우 inplements를 하더라도 추상(온전하지 않은, 객체를 생성할 수 없는) 클래스로 바뀜.
    @Override
    public void useSkill(int type) {
        switch (type) {
            case Champion.SKILL_Q:
                System.out.println("Q 스킬을 사용했습니다.");
                break;
            case Champion.SKILL_W:
                System.out.println("W 스킬을 사용했습니다.");
                break;
            case Champion.SKILL_E:
                System.out.println("E 스킬을 사용했습니다.");
                break;
            case Champion.SKILL_R:
                System.out.println("궁극기를 사용했습니다.");
                break;
        }
    }
}

/**
 * interface는 `추상 메소드로만` 이루어진 클래스를 말한다.
 * 추상 클래스와 마찬가지로 불완전한 클래스이므로 객체를 생성할 수 없다.
 * implements 키워드로 추상 메소드를 구현하게 된다.
 * 추상 클래스와 더불어 interface를 사용하는 이유는, 클래스의 구조를 잡기 위함이다(대부분의 클래스가 공통적인 기능을 수행하는 메소드를 가질 경우)
 */
interface Champion {
    // interface는 멤버변수로 스태틱 상수(Static Constant)를 사용할 수 있다. (static 변수들은 객체의 생성 유무와 관련이 없기 때문)
    int SKILL_Q = 1; // 명시하지 않아도 되지만 interface의 멤버변수들은 default로 `public static final`의 속성을 가지고 있다.
    int SKILL_W = 2;
    int SKILL_E = 3;
    int SKILL_R = 4;

    // interface의 메소드는 전부 abstract 메소드이기 때문에 키워드는 생략한다.(deafult가 public abstract)
    void useSkill(int type);
}
```

간단한 내용은 여기까지 하고 다음 시간에는 다중상속과 인터페이스에 대해서 조금 더 깊게 알아보자 이만 안녕~
