---
title: "context"
date: 2022-10-19 22:31:00 -0400
categories: react
---

Component 에서 다른 Component 로 state 를 전달해주기 위해 props 형태로 전달해줘야 한다.

두 Component 의 계층이 많이 떨어져 있는 경우에는 그 사이의 모든 Component 가 자신의 자식에게 전달하기 위해 props 를 받아야 한다.

[![context가 필요한 예](https://img.youtube.com/vi/3MB8DBXzEos/0.jpg)](https://youtu.be/3MB8DBXzEos)

이런 경우에는 Global 로 상태 관리를 하는 것이 편리할 것이다. 그러기 위해 사용하는 것이 **Context Provider** 와 **Context Consumer** 이다.

**Provider** 를 만들어서 데이터를 Context에 넣을 수 있다. **Provider** 는 Component 트리 전체나 트리 일부를 감싸는 리액트 Component이다.

**Consumer** 는 Context 에게서 데이터를 읽어오는 리액트 Component이다.

Context 를 사용하면 데이터를 사용하지 않을 여러 Component 를 거쳐서 최종 Component에 전달할 필요가 없어진다.

> Provider 가 꼭 전체 애플리케이션을 감쌀 필요는 없다. Component 트리 중 일부분만 감싸도 되고, 그렇게 하면 애플리케이션이 더 효율적으로 작동한다. 그리고 Provider 는 여러 번 사용해도 된다.

## Context 한계

---

여러 컴포넌트에 영향을 미치는 state들에 사용하기 적합하다. 하지만, 컴포넌트 구성을 대체할 수 없다.

변경이 잦은 경우에는 리액트 컨텍스트는 적합하지 않다.

리액트 컨텍스트는 1초에도 여러 번 바뀌는 경우에는 최적화되어 있지 않다.

> 전역에서 사용하고 자주 변경되는 경우에는 **리덕스**(redux)가 적합하다.

props의 모든 컴포넌트 커뮤니케이션을 대체하기 위해 사용하면 안된다.

## Context 예제(createContext, useContext, state, custom hook)

---

```javascript
export const ContextTest = createContext();

export const ContextProviderTest = () => (
  <ContextTest.Provider value={{ recipes }}>
    <ContextConsumerTest />
  </ContextTest.Provider>
);
```

**createContext** 라는 함수를 사용해 새로운 Context 객체를 만든다.
만들어진 Context 객체에는 Context Provider 와 Context Consumer 2가지 Component 가 들어있다.
Provider 의 value를 설정하면 Context에 데이터를 추가할 수 있다.

```javascript
export default function ContextConsumerTest() {
  const { recipes } = useContext(ContextTest);
  return (
    <div>
      {recipes.map((recipe, i) => (
        <span key={i} style={{ display: "block" }}>
          {recipe.name}
        </span>
      ))}
    </div>
  );
}
```

**useContext** 훅을 사용해 Context에서 데이터를 얻을 수 있다.

```javascript
const ContextTest = createContext();

export const ContextProviderTest = ({ children }) => {
  const [data, setData] = useState(recipesData);
  const addData = ({ name, ingredients, steps }) =>
    setData([...data, { name, ingredients, steps }]);
  const removeData = (name) =>
    setData(data.filter((recipe) => recipe.name !== name));

  return (
    <ContextTest.Provider value={{ data, addData, removeData }}>
      {children}
    </ContextTest.Provider>
  );
};
```

state(ex. data) 배열의 값을 변경하는 경우에 대한 함수(ex. addData, removeData...) 를 정의하여 Context에 추가하면 setData 함수를 외부에 노출하는 것을 막을 수 있고, 배열에서 허용된 값만 변경하도록 할 수 있다.

```javascript
const ContextTest = createContext();

export const useContextTest = () => useContext(ContextTest);

export const ContextProviderTest = ({ children }) => {
  const [data, setData] = useState(recipesData);
  const addData = ({ name, ingredients, steps }) =>
    setData([...data, { name, ingredients, steps }]);
  const removeData = (name) =>
    setData(data.filter((recipe) => recipe.name !== name));

  return (
    <ContextTest.Provider value={{ data, addData, removeData }}>
      {children}
    </ContextTest.Provider>
  );
};
```

```javascript
export default function ContextConsumerTest() {
  const { data, addData, removeData } = useContextTest();
  const [targetRecipe, setTargetRecipe] = useState();

  return (
    <div>
      {data.map((recipe, i) => (
        <span key={i} style={{ display: "block" }}>
          {recipe.name}
        </span>
      ))}
      <input
        type="text"
        onChange={(e) => setTargetRecipe({ name: e.target.value })}
      />
      <button onClick={() => addData(targetRecipe)}>Add</button>
      <button onClick={() => removeData(targetRecipe.name)}>Remove</button>
    </div>
  );
}
```

```javascript
export default function ContextTestPage() {
  return (
    <ContextProviderTest>
      <ContextConsumerTest />
    </ContextProviderTest>
  );
}
```

커스텀 훅(useContextTest)을 만들어서 Context 를 소비자 Component(ContextConsumerTest) 에게 노출 시킬 필요가 없도록 할 수 있다.
