## 생명주기 (Life-cycle)

> 컴포넌트는 생성(mounting) -> 업데이트(updating) -> 제거(unmounting)의 생명주기를 갖는다. <br />
> 즉, 컴포넌트는 계속 존재하는 것이 아니라, 시간의 흐름에 따라 생성되고, 업데이트 되다가 사라진다.

<img src="https://velog.velcdn.com/images%2Fminbr0ther%2Fpost%2F7f8ed738-2f24-46bd-ab9f-2c7e7d7976e2%2FUntitled-3.png" />

### 1.1. Class Componet 생명주기

### Mount
컴포넌트가 생성될 때의 생명주기를 Mount라고 한다.<br />
순서는 다음과 같다.

> 1. state, context, defaultProps 저장
> 2. **render**로 컴포넌트를 DOM에 부착
> 3. Mount가 완료된 후 **componentDidMount** 호출


**constructor(생성자)**<br />
컴포넌트의 생성자 메서드이자, 컴포넌트가 생성되면 가장 먼저 실행되는 메서드이다.<br />
this.props, this.state에 접근이 가능하고 리액트 요소를 반환한다.

```javascript
class LikeButton extends React.component {
    constructor(props){
        super(props);
        
        this.state = {
            liked: false
        }
    }
}
```

**getDerivedStateFromProps**<br />
props로부터 파생된 state를 가져온다. <br />
즉 props로 받아온 것을 state에 넣어주고 싶을때 사용한다.

**render**<br />
컴포넌트를 화면에 렌더링하는 메서드이다.

**componentDidMount**<br />
컴포넌트가 마운트 되었을 때(컴포넌트의 첫번째 렌더링이 마치면) 호출되는 메서드이다.<br />
이 메서드가 호출되는 시점에는 화면에 컴포넌트가 나타난 상태.<br />
여기서는 주로 DOM을 사용해야 하는 외부 라이브러리 연동, 해당 컴포넌트에서 필요로하는 데이터를 ajax로 요청, 등의 행위를 한다.

### Update
컴포넌트가 업데이트되는 시점이다. 
이 때 실행되는 메소드는 다음과 같다.

**getDerivedStateFromProps**<br />
컴포넌트의 props나 state가 바뀌었을때도 이 메서드가 호출된다.

**shouldComponentUpdate**<br />
컴포넌트가 리렌더링 할지 말지를 결정하는 메서드이다.<br />
React.memo와 유사하며, boolean 반환으로 결정된다.

**componentDidUpdate**<br />
컴포넌트가 업데이트 되고 난 후 발생한다.<br />
(의존성 배열이 변할때만 useEffect가 실행하는 것과 같음)


[//]: # (#### Props Update)

[//]: # (> 업데이트가 발생하였음을 감지하고, 아래의 순서대로 호출된다. <br />)

[//]: # (> 1. &#40;**componentWillReceiveProps**&#41; <br />)

[//]: # (> 2. **shouldComponentUpdate** <br />)

[//]: # (> render 이전이기 때문에 return false의 경우 render 취소&#40;성능 최적화&#41;가 가능하다. <br />)

[//]: # (> 3. &#40;**componentWillUpdate** <br />&#41;)

[//]: # (> props 업데이트 이전이기 때문에, state를 바뀌서는 안된다.)

[//]: # (> 4. render 되면 **componentDidUpdate**가 된다. <br />)

[//]: # (> 바뀌기 이전의 Props에 대한 정보를 가지고 있으며, DOM 접근이 가능하다.)

[//]: # (> )

[//]: # ()
[//]: # (#### State Update)

[//]: # (> setState 호출을 통해 state가 업데이트 될 때의 과정이다. <br />)

[//]: # (> props 업데이트와 과정이 같지만, ComponentWillReceiveProps는 호출되지 않는다.)

[//]: # (> 1. shouldComponentUpdate)

[//]: # (> 2. componentWillUpdate)

[//]: # (> 3. render)

[//]: # (> 4. componentDidUpdate <br />)

[//]: # (> 바뀌기 이전의 state의 정보를 가지고 있다.)



### Unmount

컴포넌트가 제거되는 것을 unmount라고 한다. <br />
상위컴포넌트에서 더 이상 화면에 해당 컴포넌트를 화면에 노출되지 않게 될 때 Unmount 된다.

**componentWillUnmount** <br />
더는 컴포넌트를 사용하지 않을 때 발생하는 이벤트이다. <br />
컴포넌트가 화면에서 사라지기 직전에 호출된다.<br />
DOM에 직접 등록했던 이벤트를 제거한다.<br />


### 2.1. Functional Componet 생명주기
> Hook은 함수형 컴포넌트에서 React state와 생명주기 기능을 연동할 수 있게 해주는 함수이다.

<img src="https://velog.velcdn.com/images/colagom/post/3bac93b6-60fe-45ca-9f1a-c50f464ee5c9/image.png" width="800px" />

> [Mounging]
> 1. component를 mounting 한다.
> 2. return 값을 렌더링 한다.
> 3. rendering된 상태를 가상돔에 그린다.
> 4. 가상돔과 돔의 엘리먼트들을 비교하고, 다른 부분이 감지된다면 그 부분만을 돔에 업데이트 한다. (초기 업데이트는 모든 돔에 그린다)
> 5. component 내부 useEffect, useLayoutEffect를 호출한다.

> [updating]
> 1. user의 상호작용에 의해 값이 변경된다. 
> 2. 가상돔을 변경된 props와 state에 맞추어 다시 그린다. (변경된 부분만)
> 3. component 내부 useEffect, useLayoutEffect를 호출한다.

> 컴포넌트 소멸 전, useEffect 내부 clean up 함수 실행

<details>
    <summary>자세히</summary>

- 이점
1. 기존의 라이프사이클 기반이 아닌, 로직 기반으로 나눌 수 있어 컴포넌트를 함수 단위로 잘게  쪼갤 수 있다는 이점이 있다.
2. 라이프사이클 메서드에는 관련 없는 로직이 자주 섞여 들어가는데, 이는 무결성을 해치게 된다.

- Hook 사용 규칙
1. 최상위에서만 호출해야 한다. 이 규칙을 따르면, 컴포넌트가 렌더링 될 때마다, 항상 동일한 순서로 Hook이 호출되는 것을 보장할 수 있다.
2. 일반 JS함수가 아니라, 리액트 함수 컴포넌트에서만 Hook을 호출해야 한다.

</details>


**useEffect** <br />
화면에 렌더링이 완료된 후에 수행되며componentDidMount와 componentDidUpdate, componentWillUnmount가 합쳐진 것

❗️만약 화면을 다 그리기 이전에 동기화 되어야 하는 경우에는,useLayoutEffect를 활용하여 컴포넌트 렌더링 - useLayoutEffect 실행 - 화면 업데이트 순으로 effect를 실행시킬 수 있다.

```javascript
useEffect(() => {}); // 렌더링 결과가 실제 돔에 반영된 후마다 호출
useEffect(() => {}, []); // 컴포넌트가 처음 나타날때 한 번 호출
useEffect(() => {}, [의존성1, 의존성2, ..]); // 조건부 effect 발생, 의존성 중 하나가 변경된다면 effect는 항상 재생성된다.
```

useEffect안에서의 return은 정리 함수(clean-up)를 사용하기위해 쓰여진다.
1. 메모리 누수 방지를 위해 UI에서 컴포넌트를 제거하기 전에 수행
2. 컴포넌트가 여러 번 렌더링 된다면 다음 effect가 수행되기 전에 이전 effect가 정리됩니다.