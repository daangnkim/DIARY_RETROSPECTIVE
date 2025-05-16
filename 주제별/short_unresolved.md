## 클라이언트 상태가 서버 상태를 기반으로 변경돼야 하는 경우 문제점

서버 상태를 기반으로 클라이언트 상태를 setState 하거나, 서버 상태를 mutate 한다고 가정해보자.

이때 서버 상태가 변경되어 새롭게 클라이언트 상태를 setState 하는 경우 사용자가 작성중이던 데이터가 소실될 수 있다.

이때 refetch 시간을 정해주는 staleTime과 캐싱된 데이터를 얼마나 유지할지 결정하는 gcTime을 적절히 조절해야 한다.

케이스를 몇 가지 생각해보자

1. chatGPT 사이트는 서버에 데이터를 보내기 전에 서버로부터 사용 가능한 model을 전달받는다. 만약 서버에서 내가 선택한 model이 삭제가 된 경우 어떻게 핸들링 해야할까?

2. youtube 댓글 리스트에서 특정 유저의 댓글에 댓글을 달려고 하는 경우, 만약 서버에서 내가 대댓글을 달려는 댓글이 삭제가 된 경우 어떻게 핸들링 해야할까?

## [REACT] 렌더링을 위한 콜백함수 내 파라미터 명과 로직 명이 충돌하는 경우

객체 요소를 담고있는 배열을 렌더링할 때 콜백 함수 파라미터의 키값 변수명이 충돌하는 경우가 비일비재하다.

리액트에서 다음과 같은 상황이 발생하는 경우

```javascript
const Cart = () => {
  const items = [];

  return (
    <ul>
      {items.map(({ itemId }) => {
        return (
          <li>
            <button
              onClick={() => {
                const newItems = [...items];
                newItems.filter(({ itemId }) => itemId !== itemId); // 🤯
              }}
            >
              카트에서 아이템 제거
            </button>
          </li>
        );
      })}
    </ul>
  );
};
```

property renaming을 이용하긴 하는데... 머랄까 만족스럽지 않다.

```javascript
const Cart = () => {
  const items = [];

  return (
    <ul>
      {items.map(({ itemId }) => {
        return (
          <li>
            <button
              onClick={() => {
                const newItems = [...items];
                newItems.filter(
                  ({ itemId: tempItemId }) => tempItemId !== itemId
                ); // 😇
              }}
            >
              카트에서 아이템 제거
            </button>
          </li>
        );
      })}
    </ul>
  );
};
```

## [NEXTJS] 13버전 기준으로 useSearchParams 값이 제대로 동작하지 않는 이슈

`/map?isModalOpen=true`일때, 모달 내에서 params.delete('isModalOpen')을 호출하고 router.replace(`?${params.toString()}`)을 호출하면 모달이 닫힌다.

하지만 useSearchParams의 반환값이 여전히 `isModalOpen=true`가 포함돼있다.
