# 🧡🍯 Honey-tips 

[toc]

## 행과 열을 간단히 뒤집는 방법

```python
from pandas import DataFrame

data = [
    [1, 2, 3],
    [1, 2, 3],
    [1, 2, 3],
]
data2 = []
print(DataFrame(data))

print('############################')

for ele in zip(*data):  # 세로 데이터를 포함해서 200행 짜리 데이터를 만든다
    data2.append(list(ele))
print(DataFrame(data2))
```

