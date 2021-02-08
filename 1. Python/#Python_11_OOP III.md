# 11 OOP III

> - 상속
>- 메서드 오버라이팅
> - 다중 상속 



## 11.1 상속

> 클래스의 가장 큰 특징은 `상속`이 가능하다는 것 

```python
#Person class 생성

class Person:
    population = 0
    
    def __init__(self, name='사람'):
        self.name = name
        Person.population += 1
        
    def talk(self):
        print(f'반갑습니다. {self.name}입니다.')
        
        
#Student class로 상속         
class Student(Person):
    def __init__(self, name, student_id):
        self.name = name
        self.student_id = student_id
        
s1 = Student()
```

```python
#상속관계 확인법 1

issubclass(Student, Person)  # => True

isinstance(s1, Student)  # => True
isinstance(s1, Person)   # => True

#주의
isinstance(s1, Person)  # => True, 상속 관계에 있어도 True
type(s1) is Person  # => False, 해당 클래스인 경우만 True
```



**내장 타입에도 상속 관계가 있다**

```python
#boolean은 int를 상속받아 만들어졌다

isinstance(True, int) # => True
type(True) is int # => False
```



#### `super()`

- 자식 클래스에 메서드를 추가로 구현할 수 있다.
- 부모 클래스의 내용을 사용하고자 할 때, `super()`를 사용할 수 있다.

```python
#Person class 생성

class Person:
    population = 0
    
    def __init__(self, name='사람'):
        self.name = name
        Person.population += 1
        
    def talk(self):
        print(f'반갑습니다. {self.name}입니다.')
        
        
#Student class로 상속         
class Student(Person):
    def __init__(self, name, student_id):
        super().__init__(name) #부모 클래스의 init을 실행하고 
        self.student_id = student_id #추가작업 
        
s1 = Student()
```



## 11.2 메서드 오버라이딩 

> Method Overriding(메서드 재정의): 자식 클래스에서 부모 클래스의 메서드를 재정의하는 것
>
> 상속받은 클래스에서 **같은 이름의 메서드**로 덮어쓴다

```python
#Person class 생성

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
        
    def talk(self):
        print(f'안녕, {self.name}')
        
 # Soldier class 상속

class Soldier(Person):
    def __init__(self, name, age, number, level):
        super().__init__(name, age, number)
        self.level = level
    def talk(self):       #오버라이딩
        if self.level == '참모총장':
            print('내 밑으로 집합')
        else:
            print(f'충성! {self.number}{self.name}입니다!')
```

**상속관계에서의 이름공간**

- 인스턴스 -> 자식 클래스 -> 부모 클래스 -> 전역
- 공통 사항인 것을 부모클래스에 작성하고 추가 사항은 자식 클래스에 작성한다 



## 11.3 다중 상속

- 두 개 이상의 클래스를 상속받는 경우 다중 상속이 된다
- 다중 상속 시 먼저 정의한 클래스를 받는다

```python
#Person 클래스 정의

class Person:
    
    def __init__(self, name):
        self.name = name
        
    def talk(self):
        print('사람입니다.')
        
#Mom 클래스 정의

class Mom(Person):
    gene = 'XX'
    
    def swim(self):
        print('첨벙첨벙')
        
#Dad 클래스 정의

class Dad(Person):
    gene = 'XY'
    
    def walk(self):
        print('씩씩하게 걷기')
        
#다중 상속

class FirstChild(Mom, Dad):
    #엄마와 아빠를 모두 상속받음
    
    def cry(self):
        print('응애')
        
    def walk(self):
        print('아장아장')
        
baby.gene # => 'XX'

#이 때 Dad 클래스를 앞으로 상속하면 gene이 아빠를 따르게 됨
```



