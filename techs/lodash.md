loadsh에서.

### debounce란?

특정 이벤트가 발생할때 작동하는 비즈니스 로직이 과도하게 발생하는 것을 방지하기위해 사용되는 함수이다.
input box에서 검색어를 입력할때마다 서버에서 연관된 검색어 정보를 가져와 보여주는 기능을 구현할때 주로 사용한다.
마지막 이벤트가 호출된 이후에 일정시간이 지난 후에 함수를 지연호출 시키는 역할을 한다.

```
import { debounce } from "lodash";

const getDB = debounce((item) => {
    dispatch(getPublicListMapDB(item));
    dispatch(getPrivateListMapDB(item));
    dispatch(filteringChangeCoords(item));
    setPublicPage(1);
    setPrivatePage(1);
  }, 500);


< input type="text" value={text2} onChange={(e)=>getDB(e.target.value)} />
```

이런식으로 써주면 된다.
