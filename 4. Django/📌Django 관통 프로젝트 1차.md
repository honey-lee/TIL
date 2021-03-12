# 📌Django 관통 프로젝트 1차



## 가상환경

- 파이썬 인터프리터, 라이브러리 및 스크립트가 '시스템 파이썬' (운영 체제의 일부) 설치된 모든 라이브러리와 격리되어 있는 파이썬 환경
- 각 가상 환경 (=복제본)은 고유한 파이썬 환경을 가지며 독립적으로 설치된 패키지 집합을 가짐 (목적에 따라 각 복제본을 만들어둠)
- 가상 환경 지원 시스템 
  - `venv`, `virtualenv`, `conda`, `pyenv`
- 특정 프로젝트를 위해 계정을 나눠서 사용

### 왜 사용할까?

- 호환성(dependency)!
- 협업 및 다수의 컴퓨터를 사용하는 경우 프로젝트 간 충돌을 방지하고, 버전 관리를 용이하게 하기 위함.
- pip로 설치한 패키지들은 Lib/site-packages 안에 저장되는데 이는 모든 파이썬 스크립트에서 사용할 수 있다.
- 그런데 여러 프로젝트를 진행하게 되면 프로젝트 마다 다른 버전의 라이브러리가 필요할 수도 있는데 파이썬에서는 한 라이브러리에 대해 하나의 버전만 설치가 가능하다.
- 더불어 각 라이브러리나 모듈은 서로에 대한 의존성이 다르기때문에 알 수 없는 충돌이 발생하거나 다른 여러 문제를 일으킬 수 있다.

### 명령어 

```shell
#python.exe에 있는 파일 중 / 오른쪽에 있는 모듈(venv) 실행 / 가상화 폴더의 이름 지정(venv)
$ python -m venv venv

$ source venv/Scripts/activate

#가상환경이 활성화 된 것 (venv)을 확인하고 필요한 모듈을 추가 설치
$ pip install django

#활성화 끄기
$ deactivate

#가상 환경에서 사용하고 있는 모든 라이브러리의 이름과 버전 출력
$ pip freeze

#출력결과를 따로 저장 (venv 하단에 requirements.txt 생성)
#자동으로 아래 경로 생성해서 저장 가능 
$ pip freeze > requirements.txt

#requirements에 있는 모든 파일 한번에 설치
$ pip install -r requirements.txt
```



**앞으로는**

1. 각 프로젝트 폴더에 가상환경 생성
2. `.gitignore`로 venv등 git관리 하지 않을 것들을 선언
3. `README.md` : python version 명시
4. `requirements.txt`

```MARKDOWN
# PJT 04
python version : 3.8.7
```



## Pair와 프로젝트 공유하기

`Fixture` : 초기 데이터

### 1. Push 하기 전에(보내는 사람)

1. django fixture 현재 DB  상태 복제본을 만든다

```shell
#전체 파일 뽑아오기 
$ python manage.py dumpdata --indent 4 movies.movie

#파일 생성해서 전체 영화정보 넣어주기 
$ python manage.py dumpdata --indent 4 movies.movie > movies.json

#초기데이터가 들어갈 파일 fixtures 생성 후 movies.json파일 넣음 

$ python manage.py loaddata movies/movies.json
```

2. project/fixtures/project 구조로 폴더 생성
3. fixtures 내에 movies.json파일 넣기
4. `push!`



### 2. Pull 하고 나서 (받는 사람)

모델은 만들어져있지만, dbsqlite는 git에 올리지 않았기때문에 migrate 필요!

```bash
$ python manage.py migrate # 설계도 적용, DB 생성

$ python manage.py loaddata moives/movies.json # 복제본 DB로 불러오기
```

- 단, `movies.json` 에는 영화의 `pk`도 지정되어 있기 때문에,  `load` 하기전에 create 등으로 입력한 데이터들은 덮어씌워진다. `dumpdata`는 고정되어 있는 데이터이기 때문! 구현 확인을 위한 테스트 데이터로 생각할 수 있다.

- 또한, 모델에 변경이 생겼다면 `makemigrations` 부터 다시 해줘야한다. 모델에 필드를 추가할 경우 json과 충돌이 생길 수 있는데, 이는 따로 처리가 필요하다.

- 테이블이 없다는 오류는  `migrate` 하면 해결된다.

