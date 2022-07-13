# Nuxt.js

## asyncData vs fetch

https://velog.io/@chaerin00/Nuxt-asyncData%EC%99%80-fetch%EC%9D%98-%EC%B0%A8%EC%9D%B4

### asyncData의 파라미터

참고 경로 : https://joshua1988.github.io/vue-camp/nuxt/data-fetching.html#asyncdata

* context

컨텍스트 속성은 넉스트 프레임워크 전반에 걸쳐 공용으로 사용되는 속성으로써 플러그인, 미들웨어 등의 속성에서도 접근할 수 있습니다. 컨텍스트에는 스토어, 라우터 관련 정보뿐만 아니라 서버 사이드에서 요청, 응답 관련된 속성도 접근할 수 있습니다.

## nuxt-link

예시
~~~
<nuxt-link to="/page">해당 페이지 이름으로 이동</nuxt-link>
<nuxt-link :to="{path:'page', query:{id:1}}">해당 페이지로 이동하면서 URL 파라미터를 던짐</nuxt-link>
<nuxt-link :to="{name:'page-id', params:{id:1}}">동적라우터로 이동합니다.</nuxt-link>
~~~
* query 파라미터 받기
~~~
this.$route.query
~~~

* params > 동적라우터 (/page/_id.vue)
~~~
this.$route.params
~~~

출처: https://ordinary-code.tistory.com/126 [김평범's OrdinaryCode:티스토리]


## clinet-only
SSR 페이지 내 `<client-only>` 엘리먼트로 감싸진 영역은 CSR.


## Lifecycle

### fetch
* fetchOnServer : 기본값 true. 값이 false면 client-side 에서만 호출됨. true면 server-side에서만 호출됨.

### created
* SSR 대상 컴포넌트일 경우, 총 2번 호출(SSR, CSR)
* 둘 중 한번만 호출 가능
```
created(){
  if(process.server){
    ...
  }
  또는
  if(process.client){
    ...
  }
}
```
