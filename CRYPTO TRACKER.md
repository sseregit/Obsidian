```
npm i react-router-dom@5.3.0
```

version 6 과 version 5의 문법 차이가 심하고 강의는 version 5로 진행된다.

```typescript
import {BrowserRouter, Route, Switch} from "react-router-dom";
import Coin from "./routes/Coin";
import Coins from "./routes/Coins";

function Router() {
    return (
        <BrowserRouter>
            <Switch>
                <Route path={"/:coinId"}>
                    <Coin />
                </Route>
                <Route path={"/"}>
                    <Coins />
                </Route>
            </Switch>
        </BrowserRouter>
    )
}
```

- path 추가하는법

```typescript
import {useParams} from "react-router-dom";

interface Params {
    coinId: string;
}

function Coin() {
    const { coinId } = useParams<Params>();
    return <h1>Coin : {coinId}</h1>
}
```

- Spring기준 - PathVariable을 받는법 

## Styles

1. styled-reset
```
npm i styled-reset
```

2. [Reset CSS](https://meyerweb.com/eric/tools/css/reset/)

이번강의 의 목표는 styled-component를 사용하는것 말고 전체적으로 CSS를 적용하는법을 배운다.

Fragment
- 일종의 유령 컴포넌트
- 부모 없이 서로 붙어 있는 많은 것들을 리턴할 수 있게 해준다.
```typescript
const GlobalStyle = createGlobalStyle`
	// Font는 Source Sans3를 활용한다.
	// Reset CSS를 붙여넣는다. 모든 화면에 적용됨.
`;

function App() {
    return (
        <>
            <GlobalStyle />
            <Router/>
        </>
    );
}

```
- <> </> 를 추가한다.

[flatuicolors](https://flatuicolors.com/)
- 색상을 사용할수 있다.

```javascript
(() => console.log("abc"))();

or 

() => {
	(() => console.log("function"))();
}
```
- 이 방법으로 곧바로 펑션을 호출할수도 있다.