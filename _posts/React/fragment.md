---
title: "fragment"
date: 2022-10-25 10:52:00 -0400
categories: react
---

## jsx 제한사항

---

JSX에서는 루트 요소가 1개여야 한다. 아래 소스와 같이 JSX 요소가 두개 이상인 경우에는 에러가 발생한다.

```javascript
return (
    <h2>Hi there!</h2>
    <p>This does not work.</p>
); // 에러
```

## 해결법1

---

div 태그 또는 다른 태그로 감싼다.

하지만 DOM으로 렌더링될 때 많은 컴포넌트로 중첩된 경우 불필요한 div들이 모두 렌더링된다.

```javascript
return (
  <div>
    <h2>Hi there!</h2>
    <p>This does not work.</p>
  </div>
);
```

```html
<div>
  <div>
    <div>
      <h2>Hi there!</h2>
      <p>This does not work.</p>
    </div>
  </div>
</div>
```

## 해결법2

---

JSX 요소를 배열로 반환한다. key prop도 필수적으로 입력해준다.

하지만 일반적으로 잘 사용하지 않는다. 반환 값을 배열로 만들어야 하고 모든 요소마다 key를 설정해줘야 하기 때문이다.

```javascript
return [
  <h2 key="title">Hi there!</h2>,
  <p key="contents">This does not work.</p>,
];
```

## 해결법3

---

children prop을 반환하는 빈 컴포넌트를 만들어 감싸준다. 실제로 렌더링되는 DOM에서 확인해보면 불필요한 요소없이 잘 렌더링된다.

```javascript
const Wrapper = ({ children }) => {
  return children;
};

export default Wrapper;
```

```javascript
return (
  <Wrapper>
    <h2>Hi there!</h2>
    <p>This does not work.</p>
  </Wrapper>
);
```

하지만 위와 같은 방법으로 Wrapper 컴포넌트를 별도로 만들 필요는 없다.

**리액트에서 Fragment 컴포넌트를 통해 빈 컴포넌트를 제공한다.**

두번째와 같이 빈 태그로 단축 문법을 제공한다.

```javascript
return (
  <React.Fragment>
    <h2>Hi there!</h2>
    <p>This does not work.</p>
  </React.Fragment>
);
```

```javascript
return (
    <>
        <h2>Hi there!</h2>
        <p>This does not work.</p>
    <>
);
```
