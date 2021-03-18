# Django 03

> - Form

## Form

- Form은 django 프로젝트의 주요 유효성 검사 도구들 중 하나이며, 공격 및 우연한 데이터 손상에 대한 중요한 방어 수단 (이전까지는 input 태그를 사용해 유효성 검사 없이 어떤 값이든 입력 가능했음)
- 아래 세 부분을 처리해줌
  1. 렌더링을 위한 데이터 준비 및 재구성
  2. 데이터에 대한 HTML forms 생성
  3. 클라이언트로부터 받은 데이터 수신 및 처리



## Form Class

- forms 내부의 Form class를 상속받음 (`forms.Form`, 모델 클래스 설정과 유사)
- django는 사용자의 데이터를 받을 때 해야 할 과중한 작업(데이터 유효성 검증. 필터 검증 결과 재출력, 유효한 데이터에 대해 요구되는 동작 수행 등)과 반복코드를 대신 처리해줌

```python
class ArticleForm(forms.Form):
    title = forms.CharField(max_length=10)
    content = forms.CharField(widget=forms.Textarea)
```



## Outputting form as HTML

- `as_p()` 
- `as_ul()`
- `as_table()`



## Django의 2가지 HTML input 요소 표현 방법

1. Form fields

   - input에 대한 유효성 검사 로직을 처리하며 템플릿에서 직접 사용됨

2. Widgets : django의 HTML input element 표현

   - HTML 렌더링을 처리

   - 웹 페이지의 HTML input 요소 렌더링 및 제출된 원시 데이터 추출을 처리
   - 하지만 widgets은 반드시 form fields에 할당됨
   - Form Fields는 input 유효성 검사를 처리, widgets는 웹페이지에서 input element의 단순 raw한 렌더링 처리



## ModelForm Class 작성

```python
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
    # 데이터에 대한 데이터(모델 클래스에 대한 정보 등록)
    class Meta:
        # form이 어떤 모델을 기반으로 만들어지는지 정의
        model = Article
        # field 전체를 들고오기
        fields = '__all__'
        # field에서 일부 지정하여 들고오기
        fields = ('title', 'content')
```



### Form & ModelForm

- Form
  - model에 연관되지 않은 데이터를 받을 때 사용
  - cleaned_data 딕셔너리를 생성해 정보를 받아와야 함
- ModelForm
  - django가 해당 model에서 양식에 필요한 대부분의 정보를 이미 정의
  - 어떤 레코드를 만들어야 할지 알고 있으므로 바로 `.save()` 호출 가능 



## Django View Decorators

- decorator
  - 어떤 함수에 기능을 추가하고 싶을 때, 해당 함수를 수정하지 않고 기능을 **연장**해주는 함수
- Allowed HTTP methods
  - 요청 메서드에 따라 view함수에 대한 액세스를 제한
  - 요청이 조건을 충족시키지 못하면 `HttpResponseNotAllowed`를 return
  - `require_http_methods()`, `require_GET()`, `require_POST()`, `require_safe()`

```python
# 함수 위에 데코레이터를 붙여서 사용
@require_http_methods(['GET', 'POST'])
def func(request):
```



## static

> static files(정적 파일) : 웹 사이트의 구성 요소 중에서 image, css, js파일과 같이 해당 내용이 고정되어 응답을 할 때 별도의 처리 없이 파일 내용을 그대로 보여주면 되는ㄴ 파일
>
> 즉, 사용자의 요청에 따라 내용이 바뀌는 것이 아니라 요청한 것을 그대로 응답하면 되는 파일 
>
> - 기본 static 경로 
>   - app_name/static/

![image-20210318144705484](Django 03.assets/image-20210318144705484.png)

![image-20210318144736342](Django 03.assets/image-20210318144736342.png)

```python
{% load static %}
<img src="{% static 'articles/sasmple.png' %}" alt="sample">
```



### Static Files in settings.py

- STATIC_ROOT
  - collectstatic이 배포를 위해 정적 파일을 수집하는 절대 경로
  - `collectstatic` : 프로젝트 배포 시 흩어져 있는 정적 파일들을 모아 특정 디렉토리로 옮기는 작업
- STATIC_URL
  - STATIC_ROOT에 있는 정적 파일을 참조할 때 사용할 URL
- STATICFILES_DIRS
  - app내의 static 디렉토리 경로를 사용하는 것 외에 추가적인 정적 파일 경로 정의 



## media

> 사용자가 웹에서 업로드하는 정적 파일 (image, pdf, video 등)



### Media Files in settings.py

- MEDIA_ROOT
  - 사용자가 업로드한 파일을 보관할 디렉토리의 절대 경로
  - 실제 해당 파일의 업로드가 끝나면 어디에 파일이 저장되게 할지 지정해줌
- MEDIA_URL
  - MEDIA_ROOT에서 제공되는 미디어를 처리하는 URL 
  - 업로드된 파일의 주소(url)를 만들어주는 역할
- MEDIA_URL 및 STATIC_URL은 서로 다른 값을 가져야함

```python
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/', include('articles.urls')),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```



