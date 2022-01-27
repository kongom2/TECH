# Require vs import

둘다 외부 파일이나 라이브러리를 불러올때 사용합니다. require는 nodeJS에서 사용되는 CommonJS 키워드이고, import는 ES6에서 새롭게 도입된 키워드입니다.최근 ES6(ES2015) 모듈 시스템인 import가 많이 사용되고 있지만, 아직까지는 import 키워드가 100% 대체되어 사용될 수 없습니다. `<script>` 태그를 사용하는 브라우저 환경과, NodeJS에서도 CommonJS를 기본 모듈 시스템으로 채택하고 있기 때문에, Babel과 같은 ES6 코드를 변환(transpile)해주는 도구를 사용할 수 없는 경우에는 require 키워드를 사용해야 합니다.
