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

### 함수 분리
데이터를 가져오는 용도와 가져온 데이터를 가공하는 용도를 분리하여 함수를 구현해야함.
조회와 가공을 같은 함수에서 하면 단위테스트 불가.

```
fetchBookList(){
  // 조회 API 호출 함수
  return ...
}
```
```
async getBookList(){
  // 조회 데이터 가공
  const response = await this.fetchBookList()
  this.bookList = response.bookList
}
```

### 정적 변수 관리
값 변경이 없는 변수는 data 내 선언하지 않고 import 단에 const로 선언. data에는 값 변동이 있는 변수만 적재.
```
const rowSize = 10
```

### data 내 변수 할당
* api response를 통째로 data 변수에 할당해서는 안됨. 코드 추적이 어려움. 명확하게 명시 필요.
```
this.allCnt = response.allCnt
```

### 가독성 올리기
#### 예시1
```
// 지양
this.set(this.fetchA(), this.fetchB(), ...)

// 지향
const rsltA = this.fetchA()
const rsltB = this.fetchB()

this.set(rsltA, rsltB, ...)
```

#### 예시2
```
// 지양
if( A조건 && ( B조건 || C조건 )) {

// 지향 (가독성 괜찮으면 굳이 뺄 필요 없음)
const rslt = B조건 || C조건
if( A조건 && rslt ) {
```

### boolean 값 prefix
* is~
* use~
* has~


