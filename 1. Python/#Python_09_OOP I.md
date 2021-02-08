# 09 OOP I

> Object Oriented Programming
>
> Object : 객체(컴퓨터과학)는 클래스에서 정의한 것을 토대로 메모리에 할당된 것으로 프로그램에서 사용되는 데이터 또는 식별자에 의해 참조되는 공간

> 활용 예시
>
> *** 1) 주어 동사 형식의 프로그래밍이다. *** 
>
> my_lower('Hi')   vs   'Hi'.lower()
>
> sorted([3, 2, 1]) vs ([3, 2, 1]).sort
>
> 우리가 지금까지 해온 것은 절차지향 프로그래밍에 가깝다. 
>
> *** 2) 코드의 패러다임이 변한다. ***
>
> 사람을 프로그래밍으로 표현한다면
>
> - 사람
>   - 정보
>     - 이름, 나이
>   - 행동
>     - 말하기 
>     - 먹기
>     - ....기타 등등
>
> **3) 특정 객체를 중심으로 그 객체가 일하도록 한다.**
>
> **4) 추상적인 개념을 구체화한다.**
>
> **5) 나만의 타입(Class)를 만들고 정보를 속성으로, 로직은 메서드로**





## 9.1 객체



### 타입과 인스턴스

```python
a = 10
type(a) #a는 int의 인스턴스이다
isinstance(a, int) # True
```



### 속성과 메서드

|      type |       attributes |                                methods |
| --------: | ---------------: | -------------------------------------: |
| `complex` | `.real`, `.imag` |                                        |
|     `str` |                _ | `.capitalize()`, `.join()`, `.split()` |
|    `list` |                _ |   `.append()`, `.reverse()`, `.sort()` |
|    `dict` |                _ |     `.keys()`, `.values()`, `.items()` |

- 속성 : 객체의 상태, 데이터 (사람의 이름)
- 메서드 : 조작법, (사람의 행동)

```python
# 속성
a.real     # => ()실행 문구 없이 불러옴

# 메서드

a.sort()   # => 실행하는 문구 ()가 반드시 필요
```



```python
#메서드의 chaining이 가능하다

#객체 지향
sorted(a).pop()

#절차 지향
sorted_a = sorted(a)
pop_number = sorted_a.pop()
```



```python
#list 타입의 객체들이 할 수 있는 것 
a = [1, 2, 3]

#dir 함수는 특정 객체가 할 수 있는 것을 보여준다.

print(dir(a))
# ['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```



## 9.2 객체 지향 프로그래밍

> 객체가 중심이 되는 프로그래밍
>
> 장점 : 더욱 직관적이고 수정이 용이한 코드 생성 가능 
>
> **직관성**, **용의성**, **유연성**

### 클래스와 객체

> `type`: 공통 속성을 가진 객체들의 분류(class)

> `class`: 객체들의 분류(class)를 정의할 때 쓰이는 키워드

### 1) 클래스 (사람)

- 클래스 생성은 `class` 키워드와 정의하고자 하는 이름으로 가능 
- class를 통해 새로운 type을 지정한다 
- 클래스의 이름은 `PascalCase`로 정의한다.
  - `PascalCase` : 대문자로 시작, 단어가 여러가지 합성될 경우 앞글자가 대문자인 형태
    - ex) MatterMost, PascalCase, MyClass

```python
class Person:
    pass

type(Person) #type
```

### 2) 인스턴스 (화정)

- 정의된 클래스(`class`)에 속하는 객체를 해당 클래스의 인스턴스(instance)라고 한다.
- class로부터 생성된 해당 클래스의 실체 / 예시

```python
jimin = Person() #class를 호출함으로서 생성된다
type(jimin) # =>  __main__.Person
```

### 3) 메서드 (할 수 있는 행위, 말하기 등)

- 클래스 안에 정의된 함수
- 클래스 / 인스턴스에 적용 가능한 조작법 

```python
class Person:
    
    # 클래스 내부에서 정의된 함수 => 메서드
    def talk(self):
        print('안녕')
        
iu = Person()
iu.talk()   # 안녕
Person.talk(iu) # 안녕
```



##### `self`

> **인스턴스 자신(self)**
>
> `self`라는 명칭 외에 다른 명칭도 사용 가능하나 통상적으로 `self`가 사용됨 

- Python에서 인스턴스 메서드는 **호출 시 첫번째 인자로 인스턴스 자신이 전달**되게 설계되었다.

- `self`는 가지고 있는 값을 쓸 수 있도록 표현, **호출 시 첫번째 인자로 인스턴스 자신이 전달되게 설계**
- 보통 매개변수명으로 `self`를 첫 번째 인자로 설정



### 4) 생성자 메서드 (주민등록, 출생 정보 기록)

- 인스턴스 객체가 생성될 때 호출되는 함수
- 인스턴스 속성을 정의
- `__init__`

```python
class Person:
    def __init__(self, name): #생성자 메서드
        self.name = name
        
    def talk(self):
    	return f'안녕, 나는 {self.name}'
    
    def __del__(self):   #소멸자 메서드
        return f'저는 갑니다.......{self.name}'
    
john = Person('john' #이름 지정)
              
john.talk # => '안녕, 나는 john'
```



### 5) 속성,attribute  (나이, 몸무게 등 변수)

- 클래스 / 인스턴스가 가지는 속성 (값 / 데이터)
- 인스턴스 변수

```python
class Person:
    def __init__(self, name):
        self.name = name
        
    def talk(self):
        print(f'안녕, 나는 {self.name}')
        
junsung = Person('junsung')
```



### 6) 매직메서드

- 더블언더스코어(`__`)가 있는 메서드는 특별한 일을 하기 위해 만들어진 메서드이기 때문에 `스페셜 메서드` 혹은 `매직 메서드`라고 불립니다.

- `__init__` `__str__`



