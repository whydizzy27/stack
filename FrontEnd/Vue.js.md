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

## props
* props 값은 변경 불가
* .sync 수식어
  * 양방향 바인딩(props/emit)
  ```
  // 부모
  <text-document
  v-bind:title="doc.title"
  v-on:update:title="doc.title = $event"
  ></text-document>
  
  // 자식
  this.$emit('update:title', newTitle)
  
  // 부모
  // sync를 사용하여 간소화 가능
  <text-document v-bind:title.sync="doc.title"></text-document>
  ```
  * 참고 경로 : https://kr.vuejs.org/v2/guide/components-custom-events.html

## watch
* 객체형(배열, 객체)을 그냥 watch하면 참조값만 트래킹하므로 객체 내부 속성도 트래킹하려면 deep 속성이 필요함
```
watch: {
    colours: {
      // This will let Vue know to look inside the array
      deep: true,

      // We have to move our method to a handler field
      handler()
        console.log('The list of colours has changed!');
      }
    }
  }

출처 : https://ui.toast.com/weekly-pick/ko_20190307
```

* 객체 내 속성을 개별적으로 watch

![image](https://user-images.githubusercontent.com/67194249/179866644-00b04597-666e-4933-9370-857ab0aa05b6.png)

출처 : https://codingcoding.tistory.com/337



## 인스턴스 메소드 컬럼을 특정 시점에 주입하는 법
* watch 속성을 created 훅 시점에 주입 예시
```
 created() {
    this.$watch(
      'aaa',      // 트래킹할 컬럼명
      (newVal, oldVal) => {       // 콜백 함수(매개변수는 예시로 작성함)
        // 콜백함수 로직
      },
      {           // watch 메소드 속성 추가
        immediate: true,
        deep: true
        // 등등
      }
    )
 }
```
* 장점 : 컬럼 주입 시점 컨트롤 가능
* 단점 : watch 메소드 컬럼 트래킹이 어려워짐(어디서 주입되는지..)


## provide & inject

참고 경로 : https://v3.ko.vuejs.org/guide/component-provide-inject.html

* 부모가 먼 자식에게 props 하기 위해서는 그 사이 자식 컴포넌트에게 모두 props 해야한다. 이를 편하게 하기 위해 provide, inject를 사용한다.
* 부모에서는 provide로 컴포넌트 계층 구조의 깊이와 상관없이 모든 자식에 대한 종속성 제공자 역할을 할 수 있다.

```
// 정적 값 전달하는 것은 간단하게 아래와 같이 쓰면 된다.
provide: {
  user: 'John Doe'
}

// 컴포넌트 인스턴스 속성에 접근하려면 provide를 객체로 반환하는 함수로 변환해야 한다.
data() {
  return {
    todos: ['Feed a cat', 'Buy tickets']
  }
},
provide() {
  return {
    todoLength: this.todos.length // this.todos로 data 속성에 접근
  }
}

// 자식 단 inject
inject: ['todoLength']
```
* provide/inject 바인딩이 기본적으로 반응형이 아니기 때문에 ref 속성이나 reactive 객체를 provide에 전달하여 반응형으로 변경할 수 있다.
```
// 위 소스에서 todos가 변경될 경우 todoLength가 todos의 변경을 따라가지 못한다. (반응형X)
// 아래 소스로 반응형 보장 가능.
provide() {
  return {
    todoLength: Vue.computed(() => this.todos.length)
  }
}
```
* 로그인과 같은 공통영역을 제외하면 store 대신 provide/inject를 사용하는 것이 유지보수에 좋다. 


