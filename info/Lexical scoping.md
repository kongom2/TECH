# 어휘적 범위 지정(Lexical scoping)이란?

```
function init() {
      var name = "Mozilla"; // name은 init에 의해 생성된 지역 변수이다.
      function displayName() { // displayName() 은 내부 함수이며, 클로저다.
        alert(name); // 부모 함수에서 선언된 변수를 사용한다.
      }
      displayName();
    }
    init();
```

init()은 지역 변수 name과 함수 displayName()을 생성한다. displayName()은 init() 안에 정의된 내부 함수이며 init() 함수 본문에서만 사용할 수 있다. 여기서 주의할 점은 displayName() 내부엔 자신만의 지역 변수가 없다는 점이다. 그런데 함수 내부에서 외부 함수의 변수에 접근할 수 있기 때문에 displayName() 역시 부모 함수 init()에서 선언된 변수 name에 접근할 수 있다. 만약 displayName()가 자신만의 name변수를 가지고 있었다면, name대신 this.name을 사용했을 것이다.

위 코드를 실행하면 displayName() 함수 내의 alert()문이 부모 함수에서 정의한 변수 name의 값을 성공적으로 출력한다. 이 예시를 통해 함수가 중첩된 상황에서 파서가 어떻게 변수를 처리하는지 알 수 있다. 이는 어휘적 범위 지정(lexical scoping)의 한 예이다. 여기서 `"lexical"`이란, 어휘적 범위 지정(lexical scoping) 과정에서 변수가 어디에서 사용 가능한지 알기 위해 그 변수가 소스코드 내 어디에서 선언되었는지 고려한다는 것을 의미한다. 단어 "lexical"은 이런 사실을 나타낸다. 중첩된 함수는 외부 범위(scope)에서 선언한 변수에도 접근할 수 있다.
