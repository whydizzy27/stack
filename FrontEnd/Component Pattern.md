# Component Pattern

## Container-Presenter
참고경로 : https://burning-camp.tistory.com/84

* 비지니스로직과 뷰가 한곳에 존재하게 되면 유지보수성이 떨어짐. > 비지니스로직과 뷰 분리 필요.
* Container 컴포넌트는 data와 state를 가지고 API를 호출한다. & 모든 로직을 처리한다.
* Presenter 컴포넌트는 Container에서 props 된 data를 보여줌. & state를 가지고 있지 않는 단순 함수형 컴포넌트다.
* 페이지 구성 : index < container < presenter
