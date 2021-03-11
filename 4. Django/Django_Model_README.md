# django model 복습

## Database API

### Create

```python
# 1.
article = Article()
article.title = '제에에에목'
article.content = '내애애애애용'
article.save()

# 2.
article = Article(title='제에에에목2',content='내애애애용2')
# save는 반환값이 없다

# 3.
Article.objects.create(title='제에에에목3',content='내애애애애용3')
# create는 save가 필요 없다! 바로 저장! 
# 반환 >>> 새로 생성한 정보가 담겨있는 객체 
```

### Read
```python
# 1. 전부 불러오기
articles = Article.objects.all()
print(articles)

# 2. 1개 불러오기
# pk => unique, 고유한 값!
article = Article.objects.get(pk=1)

# 3. 조건을 주고 필터링해서 불러오기
articles = Article.objects.filter(title='제에에에목')
# pk값이 2이상이면 불러오기(greater than)
lookup_article = Article.objects.filter(pk__gt=2)
# https://docs.djangoproject.com/en/3.1/ref/models/querysets/
```

### Update
```python
# 수정할 대상(객체-정보)이 있어야 함!
article = Article.objects.get(pk=1)
article.title = '이거슨 변경된 제목!'
article.content = '이거슨 변경된 내용!'
article.save()
```

### Delete
```python
# 삭제할 대상(객체-정보)이 있어야 함!
# 삭제된 pk는 다시 재사용하지 않는다
article = Article.objects.get(pk=2)
article.delete() # 끝!
```