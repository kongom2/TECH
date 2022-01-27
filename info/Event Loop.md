# Event Loop란 무엇인가?

자바스크립트는 한번에 하나의 작업만을 수행하는 싱글 스레드 언어입니다.
함수를 실행하였을때, call stack에 차곡차곡 쌓여 순차적으로 실행됩니다. 하나하나씩 작업이 이루어지다가 Web API(AJAX, setTimeout, DOM event)를 사용하는 녀석이 나오면, 이 녀석은 callback queue라는 곳에 들어가게됩니다. 그리고 이녀석은 call stack에 쌓인 모든 함수의 내용물들이 실행될때까지 대기하였다가, 모두 실행이 된 후 다시 call stack으로 push 되어서 차례대로 실행이 됩니다. 이 구조를 Event Loop라고 합니다.
