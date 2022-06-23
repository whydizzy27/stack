# refactor

## Vue.js
a태그 href 속성을 통한 화면이동보다 $router.push 사용할 것.

$router.push 사용함으로써 header, footer와 같은 다시 부를 필요 없는 레이아웃 컴포넌트를 재렌더링하지 않으므로 리소스 절약 가능
