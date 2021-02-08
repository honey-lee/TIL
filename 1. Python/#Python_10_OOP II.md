# 10 OOP II

> Object Oriented Programming
>
> Object : 객체(컴퓨터과학)는 클래스에서 정의한 것을 토대로 메모리에 할당된 것으로 프로그램에서 사용되는 데이터 또는 식별자에 의해 참조되는 공간



## 10.1 인스턴스 & 클래스 변수

### 1) 인스턴스 변수

- 인스턴스의 속성
- 각 인스턴스들의 고유한 변수
- 메서드 정의에서 `self.변수명`로 정의
- 인스턴스 생성 이후 `인스턴스.변수명`로 접근 및 할당

```python
class Person:
    def __init__(self, name): # 인스턴스 메서드 중에 특별한 생성자 메서드
        self.name = name      # 인스턴스 변수를 정의 / 할당
```

### 2) 클래스 변수

- 클래스 안에 변수를 지정 => 클래스 변수
- 모든 인스턴스가 공유
- 클래스 선언 내부에서 작동
- `클래스.변수명`으로 접근 및 할당 

```python
class Person:
    species = '사람'
    
Person.species  # => '사람'

iu = Person()
iu.species # => '사람'

iu.species = '가수'  #변경
iu.species  # => '가수'
Person.species # => '사람'
```



## 10.2 메서드의 종류

### 1) 인스턴스 메서드

- 인스턴스가 사용할 메서드
- 클래스 내부에 정의되는 메서드의 기본값은 인스턴스 메서드
- **호출 시 첫번째 인자로 인스턴스 자기자신 `self`이 전달됨**

### 2) 클래스 메서드

- 클래스가 사용할 메서드
- 클래스 단위로 사용할 메서드
- **`@classmethod`데코레이터를 사용하여 정의** 
- **호출 시 첫번째 인자로 클래스 `cls`가 전달됨**

```python
jimin = Person()
type(jimin) # __main__.Person
```

### 3)스태틱 메서드

- 아무 값도 지정하고 싶지 않을 때 사용한다. `self`도 사용하지 않음
- `@staticmethod`로 정의
- **어떤 값도 자동으로 넘겨주지 않는다**

```python
#목적에 따라 클래스, 인스턴스, 스태틱 메서드를 사용한다.

class MyClass:
    
    #인스턴스 메서드
    #가장 많이 사용되어서 데코레이터가 붙지 않는다
    def instance_method(self):
        return self
    
    #클래스 메서드
    #첫번째 인자로 cls를 받는다.
    @classmethod
    def class_method(cls):
        return cls
    
    #스태틱메서드
    #클래스 혹은 인스턴스에 접근이 필요없을 때, 정적 메서드
    @staticmethod
    def static_method(arg):
        return arg
```



### 인스턴스와 메서드

- 인스턴스는 3가지 메서드 모두에 접근할 수 있다.
- 하지만 인스턴스에서 클래스 메서드와 스태틱 메서드는 호출하지 않아야 한다. (가능하다 != 사용한다)
- 인스턴스가 할 행동은 모두 인스턴스 메서드로 한정 지어서 설계한다.

