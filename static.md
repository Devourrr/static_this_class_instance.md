###  static

클래스를 통해서 직접 인스턴스 변수 또는 인스턴스 메서드에 접근하는 건 금지되어 있다

따라해보자

"static은 클래스 소속"

"static이 없는 건 인스턴스 소속"

1. 인스턴스 변수,메서드를 다른 클래스 메서드에 호출하려면 인스턴스화를 해야한다. 

(클래스명 변수명=new 클래스명();

 2.그렇게 인스턴스화를 해서 출력한 경우, 인스턴스 변수,메서드의 Foo,f1,f2은 연동되어 있지 않기 때문에 f1의 값을 바꾼다고 해서 Foo,f2의 값은 바뀌지 않는다.  (but.클래스 변수,메서드의 경우, 연동되어있기 때문에 f1의 값을 바꾸면 주 클래스인 Foo의 값이 바뀌고 그 클래스를 사용하는 f2의 클래스 변수, 메서드의 값또한 바뀌게 된다.)



```java
class Foo{

public static String classVar = "I class var"; // 클래스 Foo에 스태틱 변수 classVar 생성 (선언)

public String instanceVar = "I instance var"; //클래스 Foo에 인스턴스 변수 instanceVar 생성 (선언)
    

public static void classMethod() { // 클래스의 스태틱 메소드가 클래스 Foo의 변수에 접근이 가능한지 확인 과정

    System.out.println(classVar); // Ok //스태틱 메소드는 클래스 Foo의 스태틱 변수 classVar에 접근 할수 있다.

    // System.out.println(instanceVar); // Error // 스태틱 메소드는 클래스 Foo의 인스턴스 변수 instanceVar에 접근 할 수없다.

}

public void instanceMethod() { // 클래스의 인스턴스 메소드가 클래스 Foo 의 변수에 접근이 가능한지 확인 과정.

    System.out.println(classVar); // Ok // 인스턴스 메소드는 클래스 Foo의 스태틱 변수 ClassVar에 접근이 가능하다.

    System.out.println(instanceVar); // Ok // 인스턴스 메소드는 클래스 Foo의 인스턴스 변수 instanceVar에 접급이 가능하다.



	}

}

public class StaticApp {

public static void main(String[] args) {

System.out.println(Foo.classVar); // OK // 클래스 Foo의 스태틱 변수에 접근이 가능하다.

// System.out.println(Foo.instanceVar); // Error // 클래스 Foo의 인스턴스 변수에 접근이 불가능 하다.



Foo.classMethod(); // 클래스 Foo의 스태틱 메소드에 접근이 가능하다.

// Foo.instanceMethod(); // 클래스 Foo의 인스턴스 메소드에 접근이 불가능하다.

Foo f1 = new Foo();

Foo f2 = new Foo();

// Foo f1,f2 인스턴스를 생성



System.out.println(f1.classVar); // I class var 클래스 Foo의 스태틱 변수 그대로 접근 가능하다.

System.out.println(f1.instanceVar); // I instance var 클래스 Foo의 인스턴스 변수 그대로 접근 가능하다.

//

f1.classVar = "changed by f1"; // 인스턴스 f1을 통해 스태틱 변수 classVar의 내용을 바꿀 경우.

System.out.println(Foo.classVar); // changed by f1 클래스 Foo의 스태틱 변수 내용을 불렀을 때 내용이 바뀐 채로 출력 된다. (원본 자체가 바뀌었다는 의미)

System.out.println(f2.classVar); // changed by f1 인스턴스 f2의 스태틱 변수 내용을 불렀을 때도 내용이 바뀐채로 출력된다. (원본 자체가 바뀌었다는 의미)



//

f1.instanceVar = "changed by f1"; // 인스턴스 f1을 통해 인스턴스 변수의 내용을 바꿀 경우.

System.out.println(f1.instanceVar); // changed by f1 인스턴스 f1의 인스턴스 변수내용을 불러냈을때, 바뀐 내용으로 출력된다. (인스턴스 f1의 내용만 바뀌었다는 의미.)



System.out.println(f2.instanceVar); // I instance var 인스턴스 f2의 인스턴스 변수 내용을 불렀을때, 인스턴스 변수 내용은 원본내용으로 출력 된다. (인스턴스 f1의 인스턴스 변수 내용을 변경해도, 스태틱변수의 내용 (원본 내용)을 변경한 것은 아니니, 인스턴스 f2에는 영향이 없다. 는 의미.)

​

	}

}
```





###  생성자와 this

"클래스와 똑같은 이름의 메소드를 정의하면 그게 바로 생성자라고 할 수 있다"

클래스와 같은 이름의 메소드를 정의하면 인스턴스를 생성할 때 

자바는 이 클래스와 동일한 이름의 메소드가 있다면 그 메소드를 호출하도록 약속되어 있다.

그 클래스가 인스턴스화 될 때 실행되어야 할 코드를 메서드 안에 정하는 걸 통해 초기화의 목적을 달성할 수 있다.

