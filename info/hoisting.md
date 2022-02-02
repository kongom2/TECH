# hoisting 이란?

함수 안에 있는 var,let,const,function과 같은 모든 선언들을 해당 함수 유효 범위의 최상단에 선언하는 것,
함수선언식은 호이스팅되지 않습니다.

변수는 3가지 단계에 의하여 생성된다.

- 선언 단계(Declaration Phase): 변수를 변수 객체(Variable Object)에 등록합니다. 이 변수 객체는 스코프가 참조하는 대상이 됩니다.
- 초기화 단계(Initialization Phase): 변수 객체(Variable Object)에 등록된 변수를 위한 공간을 메모리에 확보합니다. 이 단계에서 변수는 undefined로 초기화됩니다.
- 할당 단계(Assignment Phase): undefined로 초기화된 변수에 실제 값을 할당합니다.
  우선순위 : 변수선언 > 함수선언
