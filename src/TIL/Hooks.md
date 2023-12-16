# Component

### Class Component

- 생성자에서 state를 정의
- setState() 함수를 통해 state 업데이트(state를 이용해서 렌더링에 필요한 데이터를 관리)
- Lifecycle methods 제공


<br />

### Function Component

- state 사용 불가
- Lifecycle에 따른 기능 구현 불가

- Class Component와 차이점 📌
    - 코드가 굉장히 간결함
    - 별도로 state를 정의해서 사용하거나, 컴포넌트의 생명주기에 맞춰 어떤 코드가 실행되도록 할 수 없음
    - 이러한 함수 컴포넌트에 이런 기능을 지원하기 위해서 나온 것이 바로 Hooks!
    - 훅을 사용하면 함수 컴포넌트도 클래스 컴포넌트의 기능을 모두 동일하게 구현할 수 있게 됨 ✅

<br />

## React Hooks

React의 state와 생명주기 기능에 갈고리를 걸어 원하는 시점에 정해진 함수를 실행되도록 만들고,

이때 실행되는 함수를 hook이라고 부르기로 정한 것!

- state 관련 함수
- Lifecycle 관련 함수
- 최적화 관련 함수

<br />

### use로 시작하는 hook의 이름
hook이 수행하는 기능✅에 따라서 이름을 짓게 되었는데, 각 기능을 사용하겠다는 의미로 use✅를 붙임

<br />

## useState()
가장 대표적이고 많이 사용되는 hook, state를 사용하기 위한 훅

- 함수 컴포넌트에서는 기본적으로 state를 제공하지 않기 때문에 Class 컴포넌트처럼 state를 사용하고 싶으면 useState hook을 사용해야 함
- ❌ useState()를 사용하지 않은 코드 ❌ (엑스까지는 아니지만)


    ```javascript
    import React, { useState } from "react";

    function Counter(props) {
        var count = 0;

        return (
            <div>
                <p>총 {count}번 클릭했습니다.</p>
                <button onClick={() => count++}>
                    클릭
                </button>
            </div>    
        );
    }
    ```
    - 이렇게 count를 함수의 변수로 선언해서 사용하는 경우, 버튼 클릭 시 count값을 증가시킬 수는 있음
    - but, 재렌더링이 일어나지 않으므로 새로운 카운트 값이 화면에 표시되지 않음.

<br />

- 🔻 useState() 사용법 🔻
    ```javascript
    const [변수명, set함수명] = useState(초기값);
    ```

- useState를 노출할 때에는 파라미터로 선언할 ✅state의 초기값✅이 들어감.
- 클래스 컴포넌트의 생성자에서 state를 선언할 때 초기값을 넣어주는 것과 동일
- 이렇게 초기값을 넣어 useState를 노출하면 return 값으로 배열✅이 나옴

<br />

- return된 배열에는 두 가지 항목이 들어있음 📌
    - 첫 번째 항목은 state로 선언된 변수이고, 두 번째 항목은 해당 state의 set 함수

<br />

- ⭕ useState()를 사용한 코드 ⭕

    ```javascript
    import React, { useState } from "react";

    function Counter(props) {
        const [count, setCount] = useState(0);

        return (
            <div>
                <p>총 {count}번 클릭했습니다.</p>
                <button onClick={() => setCount(count + 1)}>
                    클릭
                </button>
            </div>        
        );
    }
    ```
    - useState✅를 사용하여 count값을 state✅로 관리하도록 만든 것
    - state의 변수명과 set함수가 각각 count, setCount로 되어 있음
        - 버튼이 눌렸을 때 setCount 함수를 호출해서 count를 1 증가 시킴✅
        - count의 값이 변경되면 Component가 재렌더링✨되면서 화면에 새로운 count값이 표시됨✨
            <br />

            이 과정은, class 컴포넌트에서 setState 함수를 호출해서 state가 업데이트 되고, 이후 컴포넌트가 재 렌더링 되는 과정과 동일하다고 볼 수 있음
            <br />

            but, class 컴포넌트에서는 setState 함수 하나로 모든 state값을 업데이트할 수 있지만,
            useState()를 사용하는 방법에서는 🖍️변수 각각에 대해 set 함수가 따로🖍️ 존재한다는 점!! 기억하기

<br />

### 🙋‍♀️ 차이 정확히 알기 🙋‍♀️

❌ useState()
```javascript
var count = 0;
```

⭕useState()
```javascript
const [count, setCount] = useState(0);
```

<br />

...

❌ useState()
```javascript
<button onClick={() => count++}>
    클릭
</button>
```

⭕useState()
```javascript
<button onClick={() => setCount(count + 1)}>
    클릭
</button>    
```

<br />

## useEffect()
useState()와 같이 가장 많이 사용되는 훅으로, Side effect를 수행하기 위한 Hook

일반적인 의미와 다르게 React에서 말하는 side effect는 그냥 효과나 영향을 뜻하는 effect의 의미에 가까움

ex) 서버에서 데이터를 받아오거나, 수동으로 DOM을 변경하는 등의 작업을 의미함

<br />

📌 그러면 왜 이런 작업을 effect라고 부를까?

: 다른 컴포넌트에 영향을 미칠 수 있고 렌더링 중에는 작업이 완료될 수 없기 때문에!✅

렌더링이 끝난 이후에 실행되어야 함❗ 때문에 이런 작업들이 side로 실행된다는 의미🖍️에서 side effect라고 불림

<br />

✅ useEffect() 훅은 React의 함수 컴포넌트에서 Side effect를 실행할 수 있게 해주는 Hook ✅

- useEffect() 훅 : 
    - class 컴포넌트에서 제공하는 생명주기 함수인 
        - componentDidMount
        - componentDidUpdate
        - componentWillUnmount와 동일한 기능을 하나로 통합해서 제공함
    - 따라서, useEffect() hook만으로 class 컴포넌트의 생명주기함수와 동일한 기능을 수행할 수 있음

    <br />

- 🔻 useEffect() 사용법 🔻
    ```javascript
    useEffect(이펙트 함수, 의존성 배열);
    ```

- 두 번째 파라미터로 들어가는 '의존성 배열'은 말 그대로, 이 이펙트가 의존하고 있는 배열.
    - ✅배열 안에 있는 변수 중에 하나라도 값이 변경✅되었을 때 '이펙트 함수'가 실행됨
    - 기본적으로 이펙트 함수는 처음 컴포넌트가 렌더링 된 이후🖍️와, 업데이트로 인한 재렌더링 이후🖍️에 실행됨.

    <br />
    
- 만약 이펙트 함수가 mount와 unmount시에 ❗단 한 번씩❗만 실행되게 하고 싶으면 아래와 같이 의존성 배열에 빈 배열을 넣으면 됨.
    ```javascript
    useEffect(이펙트 함수, []);
    ```

    - 이렇게 하면 해당 이펙트가 props나 state에 있는 어떤 값에도 의존하지 않는 것이 되므로 여러 번 실행되지 않음.

<br />

- 의존성 배열을 생략하면, 컴포넌트가 업데이트될 때마다❗ 호출 됨
    ```javascript
    useEffect(이펙트 함수);
    ```

<br />

- ⭕ useEffect()를 사용한 코드 ⭕

    ```javascript
    import React, { useState, useEffect } from "react";

    function Counter(props) {
        const [count, setCount] = useState(0);

        // componentDidMount, componentDidUpdate와 비슷하게 작동함
        useEffect(() => {
            // 브라우저 api를 사용해서 document의 title을 업데이트 함
            document.title = `You clicked ${count} times`;
        });

        return (
            <div>
                <p>총 {count}번 클릭했습니다.</p>
                <button onClick={() => setCount(count + 1)}>
                    클릭
                </button>
            </div>        
        );
    }
    ```
    
    - useEffect()를 사용해서 class 컴포넌트에서 제공하는 생명주기 함수✨의 기능을 동일하게 수행하도록 만듦.
        - 이펙트 함수 : 처음 컴포넌트가 mount되었을 때 실행되고 이후 컴포넌트가 업데이트 될 때마다 실행됨
        - 결과적으로 componentDidMount, componentDidUpdate와 동일한 역할을 하게 됨
        
        <br />

    - useEffect 안에 있는 이펙트 함수에서는 브라우저에서 제공하는 api를 사용해서 document의 title을 업데이트 함. 
        - document.title은 브라우저에서 페이지를 열었을 때 창에 표시되는 문자열을 의미함(탭에 나오는 제목)

        <br />

    - 위 코드처럼 의존성 배열 없이✅ useEffect를 사용하면 React는 DOM이 변경된 이후✅에 해당 이펙트 함수를 실행하라는 의미로 받아들임
        - 따라서, 기본적으로 컴포넌트가 처음 렌더링 될 때를 포함해서 매번❗ 렌더링 될 때마다 이펙트가 실행됨❗

        <br />

    - 또한, useEffect()는 함수 컴포넌트 안에서 선언되기 때문에 ✅해당 컴포넌트의 props와 state에 접근 가능✅
        - 위 코드에서는, count라는 state🖍️에 접근하여 해당 값이 포함된 문자열을 생성해서 사용하는 것을 볼 수 있음

<br />
<br />

📌 componentWillUnmount와 동일한 기능은 useEffect()로 어떻게 구현할 수 있을까?

```javascript
import React, { useState, useEffect } from "react";

function UserStatus(props)  {
    const [isOnline, setIsOnline ] = useState(null);

    function handleStatusChange(status) {
        setIsOnline(status.isOnline);
    }

    useEffect(() => {
        ServerAPI.subscribeUserStatus(props.user.id, handleStatusChange);
        // useEffect()의 리턴 함수의 역할은 componentWillUnmount 함수가 하는 역할과 동일
        return () => {
            ServerAPI.unsubscribeUserStatus(props.user.id, handleStatusChange);
        };
    });

    if(isOnline === null){
        return '대기 중...';
    }

    return isOnline ? '온라인' : '오프라인';
}
```

- 서버 api를 사용하여 사용자의 상태를 구독하고 있는 코드
- 이 코드에서는 함수를 하나 리턴하는데, 해당 함수 안에는 구독을 해지하는 api를 호출하도록 되어 있음.
    - useEffect에서 리턴하는 함수는 컴포넌트가 unmount될 때 호출됨.
    - 결과적으로 useEffect()의 리턴 함수의 역할은 componentWillUnmount 함수가 하는 역할과 동일한 것

<br />

⭕ useEffect()는 하나의 컴포넌트에 여러 개 사용 가능! ⭕

```javascript
function UserStatusWithCounter(props) {
    const [count, setCount] = useState(0);
    useEffect(() => {
        document.title = `총 ${count}번 클릭했습니다.`;
    });

    const [isOnline, setIsOnline] = useState(null);
    useEffect(() => {
        ServerAPI.subscribeUserStatus(props.user.id, handleStatusChange);
        return () => {
            ServerAPI.unsubscribeUserStatus(props.user.id, handleStatusChange);
        };
    });

    function handleStatusChange(status) {
        setIsOnline(status.isOnline);
    }
}
```

- 위 코드는 두 개의 useEffect 훅을 사용하고 있음
- useState hook과 useEffect hook을 각각 두 개씩 사용!
- 의존성 배열을 넣지 않았으니까 컴포넌트가 처음 렌더링될 때를 포함해서 매번 렌더링 될 때마다 이펙트가 실행됨
    - 클릭할 때마다 count값 1씩 증가
- 음.. 저 function handleStatusChange를 어떻게 쓰는건지 아직도 props랑 개념이 잘 이해가 안되네 큰일남 추가 공부 필요(til도 다시 봐라)