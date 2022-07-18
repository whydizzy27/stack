# Nuxt.js

## CSR vs SSR

### SSR 대상 화면 동작 원리
참고 경로 : https://maxkim-j.github.io/posts/nuxt-ssr

* SSR 시점 인스턴스 생성 1회
  * 프리렌더링 : 브라우저의 주소창으로 들어온 요청에 맞는 페이지 컴포넌트를 프리렌더링해 브라우저에 제공하는 방식으로 라우팅
    (HTML 파일(자바스크립트 코드 포함), store 속성 값 들어있음)
  * 하이드레이션 : 프리렌더링 과정을 마치고 브라우저로 전달된 HTML 파일 위에 남은 자바스크립트 코드들을 실행하는 동작
* CSR 시점 인스턴스 생성 1회 
  * HTML 파일을 읽고 변동 있었던 store 속성 값 적용. (단, 컴포넌트 data 속성 값은 원본 유지됨)
* created 훅은 SSR, CSR 각각 1회씩 호출됨. mounted는 CSR만.
* computed(created 훅과 동일시점), watch(immediate:true)도 SSR, CSR 각각 최초 1회 호출됨.

### CSR
* 보통 사용자 정보와 같은 개인정보는 CSR로 호출한다. (SSR로 호출 시 해당 화면을 캐싱하여 사용하기 어렵다. 개인정보는 개개인마다 다르기 때문에 공용으로 사용불가하므로.)

## asyncData vs fetch

https://velog.io/@chaerin00/Nuxt-asyncData%EC%99%80-fetch%EC%9D%98-%EC%B0%A8%EC%9D%B4

<img src="https://user-images.githubusercontent.com/67194249/178662727-ab4794f5-31d4-49e8-90f4-824d144eacfe.png" width="300" height="500">

~~내용 보완 필요~~

* asyncData 훅은 SSR 대상 페이지든 CSR 대상 페이지든 1회만 호출된다.

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

### 라우팅 CSR vs SSR
* SSR : a태그 href / nuxt-link / 브라우저 주소창에 주소입력(새로고침)
* CSR : router.push / 뒤로가기(뒤로가기는 새로고침이 아님. CSR임.)

## clinet-only
SSR 페이지 내 `<client-only>` 엘리먼트로 감싸진 영역은 CSR.


## Lifecycle

참고 경로 : https://nuxtjs.org/docs/concepts/nuxt-lifecycle/

* ~~Server 와 Client 의 Lifecycle 차이, 순서 숙지 후 내용 보완 필요~~

### fetch
* fetchOnServer : 기본값 true. 값이 false면 CSR에서만 훅 호출됨. true면 SSR에서만 훅 호출됨.
* fetch 훅 재호출 가능
```
this.$fetch()
```
재호출이 가능하다고 fetch 훅에 반복대상로직을 넣는 것은 지양하는 편이 좋다. 추후 fetch 훅에 다른 로직이 추가될 경우 문제가 된다.

### created
* SSR 대상 컴포넌트일 경우, 총 2번 호출(SSR 한번, CSR )
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

### mounted
* CSR 때만 호출


