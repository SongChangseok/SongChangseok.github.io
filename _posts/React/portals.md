# Portals

```javascript
return (
  <React.Fragment>
    <MyModal />
    <MyInputForm />
  </React.Fragment>
);
```

```html
<section>
  <h2>Some other content...</h2>
  <div class="my-modal">
    <h2>A Modal Title</h2>
  </div>
  <form>
    <label>Username</label>
    <input type="text" />
  </form>
</section>
```

DOM에 렌더링 되는 이 모달 코드는 스타일링을 제대로 하기만 하면 잘 작동한다.

하지만, 의미적인 관점이나 간결한 HTML 구조를 갖췄는지의 관점으로 보면 별로 좋지 않다.

이유는 기본적으로 모달은 모든 페이지 위에 표시되는 오버레이이기 때문에 다른 HTML 코드 안에 중첩되어 있다면 스타일링 덕분에 잘 작동할지는 몰라도 기술적으로는 좋은 코드가 아니다.

이 문제를 리애특에서 제공하는 Portal을 사용하여 왼쪽에 있는 구조를 유지한채 해결할 수 있다.

그러나 렌더링된 HTML 코드를 확인하면 JSX코드와 약간 다르다.

```javascript
return (
  <React.Fragment>
    <MyModal />
    <MyInputForm />
  </React.Fragment>
);
```

```javascript
<div class="my-modal">
    <h2>A Modal Title</h2>
</div>
<section>
    <h2>Some other content...</h2>
    <form>
        <label>Username</label>
        <input type="text" />
    </form>
</section>
```

## ReactDom.createPortal

---

포털의 핵심은 **컴포넌트에서 JSX 코드의 위치 변경 없이 렌더링된 HTML 내용을 다른 곳으로 옮기는 것이다.**

createPortal은 첫 번째 인자는 렌더링되어야 하는 리액트 노드이고, 두 번째 인자는 포인터이다.

```html
<!-- index.html -->
<div id="backdrop-root"></div>
<div id="overlay-root"></div>
<div id="root"></div>
```

```javascript
// ErrorModal.js
return (
  <>
    {ReactDOM.createPortal(
      <Backdrop onClick={onClick} />,
      document.getElementById("backdrop-root")
    )}
    {ReactDOM.createPortal(
      <ModalOverlay title={title} onClick={onClick}>
        {children}
      </ModalOverlay>,
      document.getElementById("overlay-root")
    )}
  </>
);
```
