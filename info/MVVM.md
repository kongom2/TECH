# MVVM 패턴이란?

MVVM 패턴은 Model + View + View Model를 합친 용어입니다. Model : 어플리케이션에서 사용되는 데이터와 그 데이터를 처리하는 부분입니다. View : 사용자에게 보여지는 UI 부분입니다.
View Model : View를 표현하기 위해 만든 View를 위한 Model입니다. View를 나타내 주기 위한 Model이자 View를 나타내기 위한 데이터 처리를 하는 부분입니다.

MVVM의 동작 방식은 우선, 유저의 Action이 View에 들어가고, Command Pattern으로 View Model에 Action을 전달합니다. View Model은 Model에게 데이터를 요청한 후, Model은 View Model 에게 요청받은 데이터를 응답합니다. View Model은 응답 받은 데이터를 가공하여 저장한 후, View가 View Model에 데이터 바인딩을 하여 화면을 나타냅니다.
MVVM의 View와 Model사이의 의존성이 없습니다. Command패턴과 Data Binding을 사용하여 View와 View Model 사이의 의존성 또한 없앤 디자인패턴이며, 각각의 부분은 독립적이기 때문에 모듈화하여 개발할 수 있다는 장점이 있습니다. 약간의 단점으로는 View Model의 설계가 쉽지 않다는 점이 단점입니다.
