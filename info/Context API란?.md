# Context API란?

일반적인 react 애플리케이션에서 데이터는 위에서 아래로( 즉 부모로부터 자식에게) props를 통해서

전달하는 구조로 되어있다. 간단한 프로젝트의 구조 같은 경우는 props를 전달 전달하여 값을 내려줄수 있지만

프로덕션 같은 큰 구조로 짜야져 있는경우에는 props를 전달해주는것이 번거롭고 코드가 복잡하게 구성이 되게 된다. 이러한 구조를 해결하기 위해 redux,context가 나타나게 되었는데 쉽게 생각해서 아래의 그림과 같이

별도의 상자같은곳에 코드를 작성하여 다이렉트로 해당되는 컴포넌트에 전달하는 구조로 되어있다.

![이미지](https://blogfiles.pstatic.net/MjAyMTA1MTZfMjk0/MDAxNjIxMTI3NTgxMzQ4.WoPrJ1va93ORlm5YXvP1ukXjx5yvdewxv-LdQjEPNH0g.HOc0rwjZAQS9h-TcNuQqkfo3sypbsnJ1Iow-1SrjZzMg.PNG.comingdown/image.png)

## `언제 사용하는데?`

context는 컴포넌트 안에서 전역적으로 데이터를 공유하도록 나온 개념입니다. 그런 데이터는 로그인 데이터,

web 내 사용자가 사용하는 설정파일,테마 등등 다양하게 컴포넌트 간 공유되어야 할 데이터로 사용하면 좋습니다.

## `어떻게 사용하는데?`

context api를 사용하기 위해서는 우선 createContext 를 통해 context를 생성해야 합니다.

```
const CountContext = createContext() //CountContext 사용자 정의
```

전체 코드를 통해 이해해보자

```
//CountContext.js

import React, { createContext, useContext, useState } from 'react';

const CountContext = createContext()

const CountProvier = (props) => {
    //실제 데이터 관리, 행동
    const [ cnt , setCnt ] = useState(0)

    const increment = ()  => {
        setCnt( cnt  + 1 )
    }
    const decrement = ()  => {
        setCnt( cnt - 1 )
    }

    return (
        <CountContext.Provider value={{cnt, increment, decrement}}>
            { props.children }
        </CountContext.Provider>
    );
};

export default CountProvier;

export const useCount = ()  => {
    const {cnt, increment, decrement} = useContext(CountContext)
    return {cnt, increment, decrement}
}
```

```
//Count.js

import React from 'react';
import { useCount } from '../../contexts/CountContext';

const Count = () => {
    const {cnt , increment , decrement } = useCount()

    return (
        <div>
            <h1>context 숫자: {cnt} </h1>
            <button onClick={increment}>증가</button>
            <button onClick={decrement}>감소</button>
        </div>
    );
};

export default Count;
```

```
import React from 'react';
import Count from './components/count/Count';
import CountProvier from './contexts/CountContext';

const App = () => {
  return (
    <div>
      <CountProvier>
        <Count />
      </CountProvier>
      <hr/>
    </div>
  );
};

export default App;
```
