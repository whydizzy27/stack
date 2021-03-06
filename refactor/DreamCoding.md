# DreamCoding 유튜브에서 배운 내용

## 클린코드 팁 3가지

드림코딩 유튜브 출처 : https://www.youtube.com/watch?v=jafa3cqoAVM

### DRY (Don't Repeat Yourself)
* 특정 지식, 의도, 로직 등이 다양한 곳에서 다양한 형태로 반복되는 것을 피하자는 원칙
* 단 한 곳에서 명확하고 신뢰할 수 있도록 존재해야함
* 재사용성 향상
* 변경사항 발생 시 한군데서만 수정가능 -> 유지보수성 향상
* 단순한 코드 중복만을 의미하는 것이 아닌 로직, 지식, 의도, 비즈니스로직 면에서의 광범위한 관점

### KISS (Keep It Simple, Stupid)

#### Code
* 대부분의 시스템은 복잡하게보다 심플하게 만들어졌을 때 최고로 잘 동작한다 -> 불필요한 복잡성을 피해야 함
* 열줄의 코드를 한줄의 코드로 바꾸기 위해 고도의 테크닉을 사용하여 가독성을 떨어뜨리기보다 누구나 이해할 수 있도록 심플하고 간결하게 작성하는 것이 좋음

#### Function
* 별도의 주석 없이도 함수명, 매개변수, 로직을 보고 한번에 이해할 수 있도록 한 가지 기능을 수행하는 함수를 심플하게 작성

#### Class
* 한 가지의 책임만 담당하고 있는 클래스를 심플하게 작성(그 책임과 관련 있는 변수, 함수만 포함)
* UI 담당 클래스는 UI에 관련된 로직들만 있어야 한다.(비즈니스 로직X)

#### View
* 별도의 비즈니스로직을 포함하지 않고 최대한 심플하게 UI에 관련된 로직들만 담당해야함

#### Service
* 한 가지의 기능만 담당하는 개별적이고 심플한 서비스 작성

#### => KISS한 System 구축 가능


##### 예시1
```
// isEven 에 따라 첫 짝수/홀수를 리턴하는 함수 : original
function getFirst(array, isEven){
   return array.find(x => (isEvent ? x % 2 === 0 : x % 2 !== 0));
}

// 삼항연산자를 제거해 가독성을 높이고 첫 짝수/홀수 리턴하는 별개 함수로 나눔 : refactor
function getFirstOdd(array){
   return array.find(x => x % 2 !== 0);
}

function getFirstEven(array){
   return array.find(x => x % 2 === 0);
}
```

##### 예시2
```
// original
function updateAndPrint(rawData){
   ...
}

// 기능분리함으로써 개별적으로 update와 print가 가능해짐 : refactor
function update(rawData){
   ...
}
function print(rawData){
   ...
}
```

##### 개인견해
* 가독성이 우선.
* 가독성에 따라 if else 쓸 지, 삼항연산자 쓸 지 판단하기

### YAGNI (You Ain't Gonna Need It)

1. 하지 말아야할 것들
* 필요하지 않는 기능(미래에 정말 필요할 것인가??)
* 사용하지 않는 기능(기능별로 깃 브랜치 딸 수 있으므로 사용하지 않는 코드는 주석처리가 아닌 삭제할 것)
* 지나치게 미래지향적(미래의 확장성을 위해 지나치게 범용적으로 만들지는 말 것)

2. 해야할 것들
* 깨끗하게
* 변경이 쉽게
* 유지보수 용이

-> 시스템에 불필요한 복잡성을 더하지 않는 선에서 확장성 있는 코드 작성할 것



YAGNI로 불필요한 코드를 걷어내고 KISS로 심플하게 코드를 짜자!!
