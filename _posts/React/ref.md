# ref

ref를 사용하여 렌더링되는 HTML 요소들과 자바스크립트 코드를 연결할 수 있다.

사용하기 위해서는 useRef를 호출하면 된다.

useRef가 반환한 값을 해당 컴포넌트가 렌더링하는 JSX 코드로 연결한다.

연결 방법은 ref prop을 사용하면 된다.

```javascript
const nameInputRef = useRef();
...
return (
    ...
        <input
            id="name"
            type="text"
            value={userInfo.name}
            onChange={nameChangeHandler}
            ref={nameInputRef}
        />
    ...
);
```

useRef는 항상 객체를 반환하고 current prop을 갖고 있다.

current prop은 렌더링이 되자마자 ref가 연결된 DOM 노드를 갖는다.

<img src="notion://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F5770b7df-cf03-4da4-b719-7cb43d1b3efa%2FUntitled.png?table=block&id=84bbce6d-6b7c-4cb3-9054-b995eea731e6&spaceId=20c36604-35c2-450e-9c93-ed7003b1ec4d&width=880&userId=d2758fa3-deea-4400-b632-b312c835aba7&cache=v2" />

current를 통해 조작하거나 여러 가지 작업을 할 수도 있지만

> 번거로운 작업들을 위해 리액트를 쓰기 때문에 DOM은 리액트에 의해서만 조작되어야 한다.

따라서 데이터를 읽기 정도로만 사용할 수 있다.

> state를 키 로그 기록용으로 사용하는 건 좋지 않고, 불필요한 코드와 작업이 많다.
> 따라서 값만 읽고 싶다면 ref가 더 나을 것이다.

ref를 사용할 경우 해당 컴포넌트는 제어되지 않는 컴포넌트가 된다.(리액트에 의해 제어되지 않기 때문)
