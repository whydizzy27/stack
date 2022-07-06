# Component Pattern

## Container-Presenter
참고경로 : https://burning-camp.tistory.com/84

* 비지니스로직과 뷰가 한곳에 존재하게 되면 유지보수성이 떨어짐. -> 비지니스 로직과 뷰 분리 필요
* Container 컴포넌트는 data와 state를 가지고 API를 호출한다. & 모든 로직(에러 처리 포함)을 처리
* Container에서 정의한 data와 function들을 Presenter로 props
* Presenter 컴포넌트는 Container에서 props 된 data를 보여줌. & state를 가지고 있지 않는 단순 함수형 컴포넌트
* 페이지 구성
index : import container
container : import presenter
* 
-> Container는 온전히 비지니스 로직만 / Presenter는 온전히 보여지는 view(로직의 결과)만 고려하여 유지보수의 용이성을 지니게 됨


