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

