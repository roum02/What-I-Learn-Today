## 생명주기 (Life-cycle)

> 컴포넌트는 생성(mounting) -> 업데이트(updating) -> 제거(unmounting)의 생명주기를 갖는다.

<img src="https://cdn.filestackcontent.com/ApNH7030SAG1wAycdj3H" />

### 1.1. Class Componet 생명주기

#### Mount
컴포넌트가 생성될 때의 생명주기를 Mount라고 한다.<br />
순서는 다음과 같다.

> 1. state, context, defaultProps 저장
> 2. **componentWillMount** 메소드 호출
> 3. **render**로 컴포넌트를 DOM에 부착
> 4. Mount가 완료된 후 **componentDidMount** 호출


**constructor**<br />
컴포넌트의 생성자 메서드이자, 컴포넌트가 생성되면 가장 먼저 실행되는 메서드이다.<br />
this.props, this.state에 접근이 가능하고 리액트 요소를 반환한다.

**getDerivedStateFromProps**<br />
props로부터 파생된 state를 가져온다. <br />
즉 props로 받아온 것을 state에 넣어주고 싶을때 사용한다.

**render**<br />
컴포넌트를 렌더링하는 메서드이다.

**componentDidMount**<br />
컴포넌트가 마운트 되었을 때(컴포넌트의 첫번째 렌더링이 마치면) 호출되는 메서드이다.<br />
이 메서드가 호출되는 시점에는 화면에 컴포넌트가 나타난 상태.<br />
여기서는 주로 DOM을 사용해야 하는 외부 라이브러리 연동, 해당 컴포넌트에서 필요로하는 데이터를 ajax로 요청, 등의 행위를 한다.

#### Update
컴포넌트가 업데이트되는 시점이다. 이 때 실행되는 메소드는 다음과 같다.

**getDerivedStateFromProps**<br />
컴포넌트의 props나 state가 바뀌었을때도 이 메서드가 호출된다.

**shouldComponentUpdate**<br />
컴포넌트가 리렌더링 할지 말지를 결정하는 메서드이다.

React.memo와 유사함, boolean 반환으로 결정

**componentDidUpdate**<br />
컴포넌트가 업데이트 되고 난 후 발생한다.<br />
(의존성 배열이 변할때만 useEffect가 실행하는 것과 같음)
