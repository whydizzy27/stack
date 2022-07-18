# Vue.js
## Lifecycle
### Mounted
* 자식컴포넌트부터 렌더링됨.

## Built-In Components

* component : 빌트인 컴포넌트. 동적 컴포넌트를 렌더링하기 위한 '메타 컴포넌트'라고 한다. 
* is 속성 : 문자열이나 컴포넌트 명 주입

참고 경로 : https://be-a-weapon.tistory.com/197

동적 컴포넌트 & keep-alive 사용 예시 : https://javascript.plainenglish.io/using-vue-keep-alive-component-to-save-the-state-of-dynamic-components-e52144e2260e


## keep-alive

* keep-alive로 대상 컴포넌트가 리렌더링되는 리소스를 절약할 수 있음. (비활성 컴포넌트 인스턴스를 파괴하지 않고 캐시함)
* keep-alive 엘리먼트로 둘러 쌓인 컴포넌트는 최초 생성(created)시점에 캐시되어 다른 컴포넌트에 다녀오더라도 페이지의 새로고침이 발생하기 전까지 data의 상태 유지.
* created, mounted, ..., beforeDestroy 훅은 최초 1회만 호출. destroy 훅은 호출되지 않음.  
  
  (beforeDestroy 훅 호출 시점 : router경로 이탈. ex) 상세 페이지에서 메인으로 나갔을 때 )
* activated deactivated 훅은 해당 컴포넌트 활성/비활성 때마다 호출됨. (mounted 훅 이후에 activated 훅 호출)

ex) 코딩 팁 : tab 컴포넌트 만들 때, tab 컨텐츠 중 일부만 keep-alive 적용하고 싶다 하면 일단 전체 keep-alive 로 감싼 후 keep-alive 미적용 컴포넌트의 activated 훅에서 api 호출해주면 됨.
* 킵얼라이브 태그 내 하나의 자식만 렌더링됨. v-for 사용 시 작동하지 않음.

참고 경로 : 
* https://kr.vuejs.org/v2/api/index.html
* https://velog.io/@kyusung/VUE-keep-alive
* 사용 예시 : https://sunny921.github.io/posts/vuejs-keep-alive/


## Render Function
* createElement
* JSX (React, Solid 범용 가능)
* 버튼, 아코디언과 같은 공용컴포넌트 만들 때 template 없이 Render Function 사용하는 것이 베스트.

참고 경로 : https://kr.vuejs.org/v2/guide/render-function.html


## router
### ```$router``` 객체에서 제공하는 네비게이션 메소드
참고 경로 : https://sunny921.github.io/posts/vuejs-router-03/

![image](https://user-images.githubusercontent.com/67194249/178636201-27566ca5-9a95-40a7-a69f-23234de4956e.png)

#### 예시1
* A 페이지 진입 시 세션이 없으면 자동으로 B 페이지로 라우팅시켜야 하는 경우 -> replace 사용
* push 사용 시 B 페이지에서 뒤로가기가 허용되게 되고 뒤로가기 클릭 시 A 페이지로 이동, 자동 B 페이지 라우팅하게 되므로 의미없는 라우팅 반복..


## store
### state
* 브라우저 창 간 store state는 새로고침해야 동기화된다. (새로고침 안하면 브라우저 각각 구 값, 신규 값을 가지게 됨. 즉, 구 값이 업데이트되지 않은 상태임)
