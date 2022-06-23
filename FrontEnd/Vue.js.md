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
* activated deactivated 훅은 해당 컴포넌트 활성/비활성 때마다 호출됨. (mounted 훅 이후에 activated 훅 )
* 킵얼라이브 태그 내 하나의 자식만 렌더링됨. v-for 사용 시 작동하지 않음.

참고 경로 : 
* https://kr.vuejs.org/v2/api/index.html
* https://velog.io/@kyusung/VUE-keep-alive
* 사용 예시 : https://sunny921.github.io/posts/vuejs-keep-alive/
