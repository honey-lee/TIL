# Hello, Java!

## 📌 1. 자바와 객체 지향

- 자바와 객체 지향은 뗄 수 없는 개념, 자바는 처음부터 객체 지향 언어로 만들어졌다
- `OOP` : 부품에 해당하는 객체 (Object)를 먼저 만들고 이것들을 하나씩 조립 및 연결해서 전체 프로그램을 완성하는 기법
    - 객체 지향이 잘 적용된 언어는 코드의 구조가 명확하기 때문에 코드를 이해하기 쉽고, 관리와 유지 보수가 효율적
- Java 버전 'Hello' 출력하기

```java
public class HelloWorld {
	public static void main(String[] args) {
		System.out.printIn("Hello");
	}
}
```

- Java의 함수형태

```java
리턴자료형 PrintName(파라미터자료형 파라미터) {
	함수 동작
	return 리턴값
}
```

## 📌 2. 자바와 가상머신

- ***한 번만 작성하면 어디서든 동작한다 (Wrtie Once, Run Anywhere)***
- 자바는 `호환성` 문제를 해결해준다 ▶︎ JVM만 설치되면 어느 운영체제이든 어느 디바이스이든 동일하게 동작한다
- JVM : Java Virtual Machine
- JRE : Java Runtime Environment
- JDK : Java Development Kit

## 📌 3. Hello World

- Java의 특성상 간단한 코드도 클래스 설정이 필수