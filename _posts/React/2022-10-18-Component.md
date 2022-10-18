---
title: "Component"
date: 2022-10-18 22:00:00
categories: React
---

Reusability(**재사용성**)과 **Separation of Concerns(**우려사항 분리\_\_)할 수 있도록 해주기 때문에 컴포넌트를 사용한다.

재사용 가능한 컴포넌트는 반복을 피할 수 있게 해준다.

우려사항을 분리하는 것은 코드베이스를 작고 관리 가능한 단위로 유지할 수 있게 해준다.

리액트는 재사용(re-usable) 가능하고 반응형(reactive)인 컴포넌트를 만드는데 **선언적 접근 방식**(Declarative Approach)을 사용한다.

컴포넌트가 반환하는 JSX 코드는 항상 하나의 루트 요소를 갖는다.

```javascript
function ExpenseItem() {
  return (
    <>
      <div>Date</div>
      <h2>Expense item!</h2>
      <div>amount</div>
    </>
  );
}
```

리액트는 아래의 소스와 같이 jsx의 배열을 다룰 수 있기 때문에 배열형태로 반환할 수 있다. 그래서 많은 양의 데이터를 Array.map()을 이용해 리스트 형태로 출력이 가능하다.

```javascript
const UserList = ({ items }) => {
  return (
    <Card className={styles.users}>
      <ul>
        {items.map(({ id, name, age }) => (
          <li key={id}>
            {name} ({age} years old)
          </li>
        ))}
      </ul>
    </Card>
  );
};
```

## 컴포넌트 파일 구성하기

---

컴퍼넌트 파일이 많아짐에 따라 그에 따른 파일 구성이 필요하다.

앱의 특정 기능과 관련이 없는 일반적인 사용자 인터페이스나 UI 컴포넌트와 앱의 특정 기능을 가진 컴포넌트로 나눌 수 있다.
