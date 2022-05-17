# Lambda

## &#x20;Lambda Expression

**JDK 1.8** 부터 도입된 람다로 인해 자바는 객체지향 프로그래밍 외에도 함수형 프로그래밍 또한 쉽게 지원 가능하도록 되었다. Lambda 는 메서드 자체를 식(Expression) 으로 표현하는 방법으로 이를 통해 **함수의 선언부에 관한 부분을 생략**하면서 프로그래밍이 가능하다. 그래서 이를 **익명 함수(Anonymous Function)** 이라고도 한다.

### 간결한 표현&#x20;

람다식을 이용하면 아래와 같은 상황에서는 일반적인 메소드 보다 간결하고 가독성 또한 좋다.



```java
public static void main(String[] args) { 
    IntStream intStream = IntStream.of(1,3,4,2,1,6,7);
    intStream.filter(ele -> ele != 1).forEach(System.out::println);
    intStream.filter(Example01::predicate).forEach(System.out::println);
}Ja

public static boolean predicate(int ele) {
    return ele != 1;
}
```



이미 Expression 만으로 충분히 가능하다면 Lambda 를 이용하는 것 또한 좋은 습관이다. \\

### 괄호생략&#x20;

간결한 문법의 기능 중 하나로 람다식의 Arguments 가 하나인 경우 괄호 생략이 가능하다.

`intStream.filter((ele) -> ele != 1).forEach(System.out::println);`

`// 괄호 생략 버전 intStream.filter(ele -> ele != 1).forEach(System.out::println);`

### 참조 변수 넘기기

함수형 프로그래밍이 가능하려면 함수를 인자로 받을 수 있어야 한다. \ 즉, 변수에 함수의 참조가 가능하도록 하여야 한다.&#x20;



```java
public static void main(String[] args) {
    int a = 10;
    int b = 20;

    int result = addFunction.add(a, b);
    System.out.println(result);
}

public static AddFunction addFunction = (int a , int b) -> a+b;


interface AddFunction {
    public abstract int add(int a, int b);
}
```

`}`

### 구현방법

결국엔 Java 에서 람다식 또한 클래스와 동일한데, 아래 코드를 보면 알 수 있다.

```java
intStream.filter(ele -> ele != 1).forEach(System.out::println);
intStream2.filter(new IntPredicate() { @Override public boolean test(int value) { return value != 1; } }).forEach(System.out::println);
```
