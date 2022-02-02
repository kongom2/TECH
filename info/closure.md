# Closure 란?

✅ 두 개의 함수로 만들어진 환경으로 특별한 객체의 한 종류
함수안에 함수가 있고, 이 내부함수를 return한다고 가정할때,
-> 외부 함수 호출이 종료되더라도 외부 함수의 지역 변수 및 변수 스코프 객체의 체인 관계를 유지할 수 있는 구조를 클로저라고 합니다.</br>
++ 클로저는 반환된 내부함수가 자신이 선언됐을 때의 환경(Lexical environment)인 스코프를 기억하여 자신이 선언됐을 때의 환경(스코프) 밖에서 호출되어도 그 환경(스코프)에 접근할 수 있는 함수

3줄요약하자면 다음과 같다.

1. 상태 유지
2. 전역 변수의 사용 억제 => 자신이 생성되었을 때의 lexical 환경을 기억하기 때문이다.
3. 정보의 은닉

[이곳의 예제!](https://developer.mozilla.org/ko/docs/Web/JavaScript/Closures)

```
 function makeFunc() {
      var name = "Mozilla";
      function displayName() {
        alert(name);
      }
      return displayName;
    }

    var myFunc = makeFunc();
    //myFunc변수에 displayName을 리턴함
    //유효범위의 어휘적 환경을 유지
    myFunc();
    //리턴된 displayName 함수를 실행(name 변수에 접근)
```

displayName()함수가 실행되기 전에 외부함수인 makeFunc()로부터 리턴되어 myFunc 변수에 저장된다.

```
    function makeAdder(x) {
      var y = 1;
      return function(z) {
        y = 100;
        return x + y + z;
      };
    }

    var add5 = makeAdder(5);
    var add10 = makeAdder(10);
    //클로저에 x와 y의 환경이 저장됨

    console.log(add5(2));  // 107 (x:5 + y:100 + z:2)
    console.log(add10(2)); // 112 (x:10 + y:100 + z:2)
    //함수 실행 시 클로저에 저장된 x, y값에 접근하여 값을 계산
```

본질적으로 makeAdder는 함수를 만들어내는 공장이다. 이는 makeAdder함수가 특정한 값을 인자로 가질 수 있는 함수들을 리턴한다는 것을 의미한다. 위의 예제에서 add5, add10 두 개의 새로운 함수들을 만들기 위해 makeAdder함수 공장을 사용했다. 하나는 매개변수 x에 5를 더하고 다른 하나는 매개변수 x에 10을 더한다.

add5와 add10은 둘 다 클로저이다. 이들은 같은 함수 본문 정의를 공유하지만 서로 다른 맥락(어휘)적 환경을 저장한다. 함수 실행 시 add5의 맥락적 환경에서 클로저 내부의 x는 5 이지만 add10의 맥락적 환경에서 x는 10이다. 또한 리턴되는 함수에서 초기값이 1로 할당된 y에 접근하여 y값을 100으로 변경한 것을 볼 수 있다. (물론 x값도 동일하게 변경 가능하다.) 이는 클로저가 리턴된 후에도 외부함수의 변수들에 접근 가능하다는 것을 보여주는 포인트이며 클로저에 단순히 값 형태로 전달되는것이 아니라는 것을 의미한다.

## 클로저를 이용해서 프라이빗 메소드 (private method) 흉내내기

자바와 같은 몇몇 언어들은 메소드를 프라이빗으로 선언할 수 있는 기능을 제공한다. 이는 같은 클래스 내부의 다른 메소드에서만 그 메소드들을 호출할 수 있다는 의미이다.

자바스크립트는 태생적으로는 이런 방법을 제공하지 않지만 클로저를 이용하여 프라이빗 메소드를 흉내내는 것이 가능하다. 프라이빗 메소드는 코드에 제한적인 접근만을 허용한다는 점 뿐만 아니라 전역 네임 스페이스를 관리하는 강력한 방법을 제공하여 불필요한 메소드가 공용 인터페이스를 혼란스럽게 만들지 않도록 한다.

아래 코드는 프라이빗 함수와 변수에 접근하는 퍼블릭 함수를 정의하기 위해 클로저를 사용하는 방법을 보여준다. 이렇게 클로저를 사용하는 것을 모듈 패턴이라 한다.

```
var counter = (function() {
      var privateCounter = 0;
      function changeBy(val) {
        privateCounter += val;
      }
      return {
        increment: function() {
          changeBy(1);
        },
        decrement: function() {
          changeBy(-1);
        },
        value: function() {
          return privateCounter;
        }
      };
    })();

    console.log(counter.value()); // logs 0
    counter.increment();
    counter.increment();
    console.log(counter.value()); // logs 2
    counter.decrement();
    console.log(counter.value()); // logs 1
```

## 클로저 스코프 체인

모든 클로저에는 세가지 스코프(범위)가 있다:

지역 범위 (Local Scope, Own scope)
외부 함수 범위 (Outer Functions Scope)
전역 범위 (Global Scope)
따라서, 우리는 클로저에 대해 세가지 범위 모두 접근할 수 있지만, 중첩된 내부 함수가 있는 경우 종종 실수를 저지른다. 아래 예제를 확인해보자:

```
// 전역 범위 (global scope)
    var e = 10;
    function sum(a){
      return function(b){
        return function(c){
          // 외부 함수 범위 (outer functions scope)
          return function(d){
            // 지역 범위 (local scope)
            return a + b + c + d + e;
          }
        }
      }
    }

    console.log(sum(1)(2)(3)(4)); // log 20

    // 익명 함수 없이 작성할 수도 있다.

    // 전역 범위 (global scope)
    var e = 10;
    function sum(a){
      return function sum2(b){
        return function sum3(c){
          // 외부 함수 범위 (outer functions scope)
          return function sum4(d){
            // 지역 범위 (local scope)
            return a + b + c + d + e;
          }
        }
      }
    }

    var s = sum(1);
    var s1 = s(2);
    var s2 = s1(3);
    var s3 = s2(4);
    console.log(s3) //log 20
```
