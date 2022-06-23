# Nuxt.js

## asyncData vs fetch

https://velog.io/@chaerin00/Nuxt-asyncData%EC%99%80-fetch%EC%9D%98-%EC%B0%A8%EC%9D%B4

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
