---
layout: "post"
title: "One line a day"
date: "2017-01-10 22:14"
---

## 하루에 한 줄

새해를 맞이하여 시작하는 하루에 한 줄 기록장. 언제까지 할진 나도 몰라 일단 시작

> 인생에서의 성공은 어떤 지위에 올랐느냐가 아니라, 장애물을 극복하며 성공하려고 노력하는 과정에 있다. -보커 T. 워싱턴-

### JAVA
- `main() 메소드`는 사용자가 직접 호출하는 것이 아니라 **JVM(자바 가상 머신)**에 의해 호출된다. 컴파일된 자바 파일을 실행하면 JVM은 main()부터 실행시킨다.

- `static` 으로 선언된  멤버 변수는 프로그램 내에서 단 하나의 메모리만을 차지한다. 동일한 객체의 인스턴스는 하나의 static 변수를 공유한다.(동기화의 문제) 객체를 생성하기 전에 `ClassName.foobar`로 접근할 수 있으며, 객체 생성 이전에 메모리가 생성이된다.(클래스 이름을 언급한 순간) static 메서드 내에서 일반 멤버 변수를 사용할 수 없다.(static 멤버 변수만 사용 가능) 메모리 생성 시점과 같이 생각해보면 이해가 쉽다.

- `컴파일`이란 작성된 프로그램 자체를 기계어로 변경하는 것
  - 바이트 코드: .java 파일을 컴파일 할 때 만들어지는 .class 파일(완전한 기계어는 아니고 중간 단계의 언어)

  - 자바로 프로그램을 작성하고 컴파일을 하면 기계어가 재해석하기 쉬운 중간단계의 언어인 바이트코드(.class)로 변환되고 JVM이 바이트 코드를 기계어로 해석한 후 실행하게 된다.


- Stack 메모리 영역: 프로그램을 실행하는데 필요한 메모리 공간(정적인 개념의 메모리)
  -ex)프로그램을 실행시키면 main()메서드를 실행시키고 해당 함수 안에 있는 sum()을 실행시킨다고 가정한다면, 다음과 같이 쌓일 것이다.

| Stack 메모리영역   | |
| :-------:        | |
|  ...             | |
| sum()            | 하나의 메소드에 필요한 메모리 덩어리를 `스택 프레임`이라고 한다.<br />(메소드를 호출하면 생김) |
| main()           | 지역변수, 매개변수, 리턴값을 위한 공간 <br />(호출이 끝나면 자동으로 이 스택 프레임이 제거된다.)|

- 가비지 콜렉터(GC) : JVM 내에서 더 이상 사용되지 않는 메모리나 불필요한 메모리를 제거, 메모리 조각모음 작업도 한다. JVM에 의해서 자동으로 이루어지기 때문에 메모리가 언제 정리되는지는 알 수 없음

- 오버로딩(Overloading): 동일한 이름으로 함수를 여러개 만들어서 사용할 수 있다. 이때 컴파일러는 실제로 메모리에 다른 이름으로 저장한다.(단, 매개변수의 갯수와 매개변수의 형은 달라야 한다.)

- 생성자: 객체의 메모리 생성과 동시에 자동으로 호출되는 메소드
  - Test test = new `Test()`

  - 모든 클래스는 기본적으로 생성자를 가져야하며, 따로 명시한 생성자가 없을 경우 컴파일러는 클래스 이름과 동일한 `디폴트 생성자`를 만든다.

  - 생성자의 특징
    - 리턴 타입이 없다.
    - 클래스 이름과 동일하다
    - 생성자는 객체의 메모리 생성 직후 호출된다.(사용자가 임의로 호출할 수 없다. this와 super를 이용하는 경우를 제외하고)
    - 주로 객체 생성 후 필요한 초기화 작업을 한다.


- `상속`을 받을 경우 부모 클래스 > 자식 클래스의 생성자 순으로 호출되며 멤버 메소드는 상속 받지만 생성자는 상속 받지 않는다.

- this()
  1. this는 생성자를 포함하여 생성되는 메소드가 만들어질 때 컴파일러가 자동으로 추가하는 첫번째 매개변수이며, 자기 자신을 참조하는 가상의 매개변수이다.(그렇기 때문에 멤버 메소드 내에서만 사용이 가능하다)
  2. 지역변수와 멤버 변수를 구분할 때 사용한다. `this.name = name;` (클래스 내에서 멤버변수를 사용한다면 this는 명시하지 않아도 무방하다.)
  3. this를 독자적으로 사용한다면, 자신의 참조값 자체를 의미한다.
  4. `this(optionalParam);` 은 생성자를 호출하며, 해당 매개변수 형식에 맞는 생성자를 호출한다.

  ```java
  public class Test {
      private String firstName;
      private String lastName;

      public Test(String firstName) {
          this.firstName = firstName;
          System.out.println("firstName is " + firstName);
      }

      public Test(String firstName, String lastName) {
          this(firstName);
          this.lastName = lastName;
          System.out.println("my name is " + firstName + " " + lastName);
      }

      public static void main(String... args) {
          Test father = new Test("Hwanik", "Kim");
      }
  }
  ```

    - this를 이용한 생성자 호출은 다른 어떤 작업보다 선행되어야 하기 때문에, this()호출 이전에 다른 작업도 할 수 없다.

- super: 상위 클래스를 참조할 수 있는 가상의 참조 변수
  - 오버라이딩(Overiding)을 할 때 부모 클래스의 해당 메소드는 무시된다. 그러나 본래 부모의 메소드를 사용하고자 할때는 super.foobar()로 접근하면 된다.
  - 하위 클래스의 인스턴스를 생성하기 위해서는 부모 클래스의 생성자가 호출된 후에 자식 클래스의 생성자가 호출된다. 하지만 매개변수가 있는 생성자라면?

```java
public class SuperFather {
    private String name;

    public SuperFather(String name) {
        this.name = name;
        System.out.println("call father");
    }

    public void getName() {
        System.out.println("father name is " + name);
    }
}

class SuperSon extends SuperFather {
    private String name;

    public SuperSon(String name) {
        /**
         * 부모 클래스에 매개변수가 없는 default 생성자가 있다면 매개변수가 있는 생성자는 선택적으로 호출하면 된다.
         * 부모 클래스가 default 생성자 없이 매개변수를 갖는 생성자만 있다면(설계의 문제이거나) 기능적으로 부모 클래스의 생성자가 올바르게 호출되는지 확인할 필요가 있다.
         */
        super(name);
        this.name = name;
    }

    public void getName() {
        super.getName();
        System.out.println("son name is " + name);
    }

    public static void main(String[] args) {
        SuperSon son = new SuperSon("tta");
        son.getName();
    }
}
```

- 모든 클래스는 Object(최상위 클래스)를 상속받는다. `extends Object`

- 다운 캐스팅 : 업캐스팅 된 객체를 다시 원래의 클래스로 형변환 시켜주는 작업.

- 쓰레드(Thread): 쓰레드는 하나의 프로세스 내에서 `동시에` 여러 동작을 수행하기 위한 `메소드(기능)`의 단위이다.
