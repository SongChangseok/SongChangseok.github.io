---
title: "hooks"
date: 2022-10-26 23:18:00 -0400
categories: react
---

## Hooks

---

Hook은 함수 컴포넌트에서 **React.state와 생명주기 기능(Lifecycle features)을 "연동(hook into)"할 수 있게 해주는 함수**이다. Hook은 class 안에서는 동작하지 않는다. 대신 class 없이 React를 사용할 수 있게 해주는 것이다.

## Hooks의 규칙

---

1. 리액트 함수에서만 호출해야 한다.
   - 리액트 컴포넌트 함수
   - 커스텀 훅스
2. 컴포넌트 함수 또는 커스텀 훅의 최상위 수준에서만 호출해야한다.
   - 중첩 함수에서 훅 호출 X
   - block문에서 호출 X

> useEffect 내부에는 항상 참조하는 모든 항목을 의존성으로 추가해야 한다.
