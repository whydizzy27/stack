# refactor
* if 사용 시 else 사용 최소화. return 활용.

## Vue.js
### 라우팅
* a태그 href 속성을 통한 화면이동보다 $router.push 사용할 것.
* $router.push 사용함으로써 header, footer와 같은 다시 부를 필요 없는 레이아웃 컴포넌트를 재렌더링하지 않으므로 리소스 절약 가능

### addEventListener & removeEventListener
* keep-alive 대상이어도 각각 mounted, beforeDestroy 훅에 선언하는 것이 맞음.
* activated, deactivated 훅에 add/remove 를 선언하게 되면 keep-alive를 사용하는 의미가 없음.

### Browser
* 전 페이지 스크롤 위치 유지(스냅샷)는 브라우저 기능이다. keep-alive와 관련 없음.
