## 07 Data_structure_II

- 알고리즘에 빈번히 활용되는 순서가 없는 데이터 구조 (순회 가능하지만 순서가 없다)
  - Set
  - Dictionary

### 7-1. 세트(Set)

### 추가 및 삭제

#### `.add(elem)`

#### `.update(elem)`

- Tuple 형태로 업데이트 가능
- string 형태로 업데이트 시 한 글자씩 쪼개짐

#### `.remove(elem)`

#### `.discard(elem)`

- elem을 세트에서 삭제하고 에러가 발생하지 않음
- 경우에 따라 에러를 발생시켜야 할 필요도 있음

#### `.pop()`

- 괄호 안의 원소를 제거 , 빈 괄호일 경우 임의의 원소 제거 



### 7-2. 딕셔너리 (Dictionary)

> mutable,  unordered, iterable
>
> `Key:Value` 페어의 자료구조

### 추가 및 삭제 

#### `.pop()`

- 디폴트 인자 설정가능 

#### `.update()`

- 값을 제공하는 key, value 형태로 덮어쓴다
- key를 기준으로 value를 추가 혹은 수정 가능 (없는 값은 추가, 기존에 있는 값은 수정) 



### 딕셔너리 순회 (반복문 활용)







