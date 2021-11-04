# Vue

## 📌 SFC

### 1. Component

- 기본 HTML 엘리먼트를 확장하여 재사용 가능한 코드를 캡슐화 하는데 도움을 줌
- CS에서는 다시 사용할 수 있는 범용성을 위해 개발된 소프트 웨어 구성 요소를 의미
- 한 화면을 구성하는 여러 컴포넌트 (기능별로 나눠서 준비함)

### 2. SFC (Single File Component)

- Vue의 컴포넌트 기반 개발의 핵심 특징
- 하나의 컴포넌트는 .vue라는 하나의 파일 안에서 작성되는 코드의 결과물
- 화면의 특정 영역에 대한 HTML, CSS, JavaScript 코드를 **하나의 파일 (`.vue`)에서 관리**
- 즉 `.vue` 확장자를 가진 싱글 파일 컴포넌트를 통해 개발하는 방식
- Vue 컴포넌트 === Vue 인스턴스 === .vue 파일

## 📌 Vue CLI

- Vue.js 개발을 위한 표준 도구
- 프로젝트의 구성을 도와주는 역할을 하며 Vue 개발 생태계에서 표준 tool 기준을 목표로 함
    - 확장 플러그인, GUI, ES2015 구성 요소 제공 등 다양한 tool 제공

### 1. Node.js

- 자바스크립트를 **브라우저가 아닌 환경에서도 구동할 수 있도록 하는** 자바스크립트 런타임 환경
    - 브라우저 밖을 벗어날 수 없던 자바스크립트 언어의 태생적 한계를 해결
- 단순히 브라우저만 조작할 수 있던 자바스크립트를 SSR에서도 사용 가능하게 함
- `NPM` : Node.js를 위한 패키지 관리자
    - Python의 pip와 같은 역할
    - pip와 마찬가지로 다양한 의존성 패키지를 관리
    - Vue CLI 설치 명령어
    
    ```jsx
    // vue-cli 설치
    $ npm install -g @vue/cli
    
    // 버전 확인
    $ vue --version
    
    // 프로젝트 생성
    $ vue create my-first-vue-app
    
    // run server
    $ npm run serve
    ```
    

### 2. Babel & Webpack

1. `Babel`
- JavaScript Transcompiler
- 자바스크립트의 신버전 코드를 구버전으로 번역 / 변환해주는 도구
- 자바스크립트 역사에 있어서 파편화와 표준화의 영향으로 작성된 코드의 스펙트럼이 매우 다양
    - 최신 문법을 사용해도 브라우저 버전별로 동작하지 않는 상황이 발생
    - 같은 의미의 다른 코드를 작성하는 등의 대응이 필요해졌고 이러한 문제를 해결하기 위한 도구
- 원시 코드를 목적 코드로 옮기는 번역기
- Babel 동작 예시

```jsx
// Babel Input: ES2015 arrow function
[1, 2, 3].map((n) => n + 1);

// Babel Output: ES5 equivalent
[1, 2, 3].map(function(n) {
	return n + 1;
});
```

2. `Webpack`

- static module bundler
    - 모듈 간의 의존성 문제를 해결하기 위한 도구
- Module : 파일 하나를 의미 → 모듈 단위의 개발이 활성화되면서 모듈의 의존성 문제 발생 → **Webpack은 모듈 간의 의존성 문제를 해결하기 위해 존재하는 도구**
- Bundler : 모듈 의존성 문제를 해결해주는 작업이 Bundling, 이러한 일을 해주는 도구가 Bundler이고 Webpack은 다양한 Bundler 중 하나
    - 모듈들을 하나로 묶어주고 묶인 파일은 하나로 만들어짐
    - Vue CLI는 이러한 Babel, Webpack에 대한 초기 설정이 자동으로 되어있음

### 3. Vue CLI 구조

- `src/assets` : webpack에 의해 빌드된 정적 파일
- `src/components` : 하위 컴포넌트들이 위치
- `src/App.vue` : 최상위 컴포넌트
- `src/main.js` : webpack이 빌드를 시작할 때 가장 먼저 불러오는 entry point
- `babel.config.js` : babel 관련 설정이 작성된 파일
- `package.json`
    - `scripts` : 사용할 명령어 script
    - `dependencies` : 개발 + 배포 환경에서까지 활용할 모듈
    - `devDependencies` : 개발 단계에서만 활용할 모듈
- `package-lock.json` : node_modules에 설치되는 모듈과 관련해서 모든 의존성을 설정 및 관리, 개발 과정 간의 의존성 패키지 충돌 방지

### 4. Pass Props & Emit Events

- 컴포넌트는 부모 - 자식 관계에서 가장 일반적으로 함께 사용하기 위함
- 부모는 자식에게 데이터를 전달 (Pass props) 하며 자식은 자신에게 일어난 일을 부모에게 알림 (Emit event)

![Vue%20b0f6551f15da49378a8b09edfe584a61/Untitled.png](Vue%20b0f6551f15da49378a8b09edfe584a61/Untitled.png)

1. **Props**
    - 상위 컴포넌트의 정보를 전달하기 위한 사용자 지정 특성
    - 하위 컴포넌트는 props 옵션을 사용하여 수신하는 props를 명시적으로 선언해야함
    - 즉 데이터는 props 옵션을 사용하여 하위 컴포넌트로 전달됨
    - 주의 : 하위 컴포넌트의 템플릿에서 상위 데이터를 직접 참조할 수 없음
    - 이름 컨벤션
        - in HTML : kebab-case
        - in script : camelCase
2. **Emit event**
    - `$emit(event)` : 현재 인스턴스에서 이벤트를 트리거, 추가 인자는 리스너의 콜백 함수로 전달
    - 부모 컴포넌트는 자식 컴포넌트가 사용되는 템플릿에서 v-on을 사용하여 자식 컴포넌트가 보낸 이벤트를 청취
    - 컴포넌트 및 props와는 달리, 이벤트는 자동 대소문자 변환을 제공하지 않음
    - HTML의 대소문자 구분을 위해 DOM 템플릿의 v-on 이벤트 리스너는 항상 자동으로 소문자 변환되기 때문에 이벤트 이름에 kebab-case를 사용하는 것을 권장
    

## 📌 Vue Router

vue router 설치 : `vue add router`

- `router-view` : 실제 component가 DOM에 부착되어 보이는 자리를 의미, router-link를 클릭하면 해당 경로와 연결되어 있는 index.js에 정의한 컴포넌트가 위치
    - `DOM` : Document Object Model, XML이나 HTML 문서에 접근하기 위한 일종의 인터페이스
- History mode : 브라우저의 히스토리는 남기지만 실제 페이지는 이동하지 않는 기능을 지원
    - 뒤로 가기, 앞으로 가기를 가능하게 함
- Vue Router 가 필요한 이유
    1. SPA 등장 이전
        - 서버가 모든 라우팅을 통제
        - 요청 경로에 맞는 HTML을 제공
    2. SPA 등장 이후
        - 서버는 index.html 하나만 제공
        - 이후 모든 처리는 HTML 위에서 JS 코드를 활용해 진행
        - 즉, 요청에 대한 처리를 더 이상 서버가 하지 않음
    3. 라우팅 처리 차이
        - SSR : 라우팅에 대한 결정권을 서버가 가짐
        - CSR : 클라이언트는 더 이상 서버로 요청을 보내지 않고 응답받은 HTML 문서 안에서 주소가 변경되면 특정 주소에 맞는 컴포넌트를 렌더링, 라우팅에 대한 결정권을 클라이언트가 가짐

## 📌 Lifecycle hook

- `beforeCreate` : 가장 먼저 실행되는 훅, Vue 인스턴스 초기화된 직후에 발생, 컴포넌트가 DOM에 추가되기도 전이어서 `this.$el` 에 접근할 수 없음, `data, methods`에도 접근할 수 없음
- `created`  : `data`를 반응형으로 추적할 수 있게 되며 `computed, methods, watch` 등이 활성화되어 접근이 가능, 아직 DOM에 추가되지 않은 상태
- `beforeMount` : DOM에 부착하기 직전에 호출되는 훅, 가상 DOM이 생성되어 있으나 실제 DOM에 부착되지 않은 상태
- `mounted` : 일반적으로 가장 많이 사용됨, 가상 DOM이 실제 DOM에 부착되고 난 이후 실행되므로 `this.$el`을 비롯한 `data, computed, methods, watch` 등 모든 요소에 접근 가능
    - 일반적인 경우의 부모와 자식 컴포넌트 간의 mounted 훅 순서 (자식 컴포넌트 먼저)
    
    ![Vue%20b0f6551f15da49378a8b09edfe584a61/Untitled%201.png](Vue%20b0f6551f15da49378a8b09edfe584a61/Untitled%201.png)
    
- `beforeUpdate` : 컴포넌트에서 사용되는 `data`의 값이 변해서 DOM에도 그 변화를 적용시켜야할 때 호출되는 훅, 변할 값을 이용해 가상 DOM을 렌더링하기 전이지만 이 값을 이용해 작업 가능
- `updated` : 가상 DOM을 렌더링하고 실제 DOM이 변경된 이후에 호출되는 훅, 변경된 `data`가 DOM에도 적용된 상태, 변경된 값들을 DOM을 이용해 접근하고 싶다면 가장 적절한 훅
- `beforeDestroy` : 해당 인스턴스가 해체되기 직전에 호출되는 훅, 아직 해체되기 전이므로 인스턴스는 완전하게 작동하기 떄문에 모든 속성에 접근이 가능
- `destroyed` : 인스턴스가 해체되고 난 직후에 호출되는 훅, 해체가 끝난 이후기 때문에 인스턴스의 속성에 접근 불가, 하위 Vue인스턴스 역시 삭제됨

![Vue%20b0f6551f15da49378a8b09edfe584a61/Untitled%202.png](Vue%20b0f6551f15da49378a8b09edfe584a61/Untitled%202.png)

## 📌 Vuex

- Vuex는 Vue.js 애플리케이션에 대한 `상태 관리 패턴 + 라이브러리` 이다. 애플리케이션의 모든 컴포넌트에 대한 `중앙 집중식 저장소`역할을 하며 예측 가능한 방식으로 상태를 변경할 수 있다. 또한 Vue의 공식 devtools 확장 프로그램과 통합되어 설정 시간이 필요없는 디버깅 및 상태 스냅 샷 내보내기 / 가져오기와 같은 고급 기능을 제공한다.
- 규모가 큰, 컴포넌트 간의 중첩이 깊어지는 프로젝트 설계 시 사용하면 유리
- 컴포넌트의 공유된 상태를 추출하고 이를 전역에서 관리함
- 컴포넌트는 커다란 뷰가 되며 모든 컴포넌트는 트리에 상관없이 액세스하거나 동작을 트리거할 수 있음

![Vue%20b0f6551f15da49378a8b09edfe584a61/Untitled%203.png](Vue%20b0f6551f15da49378a8b09edfe584a61/Untitled%203.png)

### 1. Vuex core concept

- 단방향 데이터 흐름
- 상태는 앱을 작동하는 원본 소스
- 뷰는 상태의 선언적 매핑
- 액션은 뷰에서 사용자 입력에 대한 반응으로 상대를 바꾸는 방법

![Vue%20b0f6551f15da49378a8b09edfe584a61/Untitled%204.png](Vue%20b0f6551f15da49378a8b09edfe584a61/Untitled%204.png)

### 2. Vuex 구성 요소

1. State
    - 중앙에서 관리하는 모든 상태 정보 (data)
    - Mutations에 의해 정의된 메서드에 의해 변경
    - 여러 컴포넌트 내부에 있는 특정 state를 중앙에서 관리
    - state가 변화하면 해당 state를 공유하는 컴포넌트의 DOM은 알아서 렌더링
2. Actions
3. Mutations
4. Getters

![Vue%20b0f6551f15da49378a8b09edfe584a61/Untitled%205.png](Vue%20b0f6551f15da49378a8b09edfe584a61/Untitled%205.png)