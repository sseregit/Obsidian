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

## [Crpto Icon API](https://coinicons-api.vercel.app/)
- 암호화폐 아이콘을 가져올수 있음.

## State
- 비하인드 더 씬 소통
- Link 경로 간에 데이터를 전달하고 받는법
```typescript
	<Link to={{
		pathname:`/${coin.id}`,
		state: { name:coin.name}
	}}>
	</Link>
```

```typescript
    const location = useLocation();
    console.log(location);
```
- 해당 state를 확인할수 있다.

## TypeScript Interface 생성 Tip

1. 해당 Json을 console.log()로 찍는다.
2. 해당 결과를 마우스 우측 클릭 *전역변수로 Object 저장*한다.
```typescript
// key를 가져오는법
Object.key(저장한 Object).join();

// value의 type을 가져오는법
Object.values(저장한 Object).map(v => typeof v);
```
3. 모든키가 , 구분자로 나오게 된다.


Hooks
- 최선의 성능을 위해서 hook 안에서 사용한 것은 그게 어떤 것이든 dependency에 넣어야 한다고 한다.

```typescript
state?.name
```
- state가 존재 하는 경우에만 name을 찾는다.

## Nested router or Nested Route
- route안에 있는 또 다른 route
- 스크린 안에 섹션이 나뉘어진곳 or TaB등

## UseRouteMathch
- 특정한 URL에 있는지의 여부를 알려준다.

## React Query
```typescript
import {QueryClient, QueryClientProvider} from "react-query";

const queryClient = new QueryClient();

root.render(
    <QueryClientProvider client={queryClient}>
        <ThemeProvider theme={theme}>
            <App/>
        </ThemeProvider>
    </QueryClientProvider>
);
```
- 스스로 실행하고 있었던 로직들을 축약해준다.
- 사용법
	1.  fetcher함수를 만든다.
		1. fetcher 함수란 fetch를 통해 api등을 호출하는것
		2. fetcher함수는 꼭 fetch promise를 return 해야한다.
```typescript
export function fetchCoins() {
    return fetch("https://api.coinpaprika.com/v1/coins")
        .then((response) => response.json());
}	
```

		2. useQuery
			1. 2가지의 argument를 필요로한다.
				1. queryKey
					1. query의 고유 식별자
				2. fetcher 함수
```typescript
const { isLoading, data} = useQuery("allCoints", fetchCoins);
```
- react query는 데이터를 캐시에 저장해둔다.
	- 또다시 로딩이 생기지 않는 이유
- 좀더 시각화 하기위해서 **Devtools**를 가지고있다.
	- render할 수 있는 component이다.
	- Import 해오면 캐시에 있는 query를 볼수 있다.
```typescript
function App() {
    return (
        <>
            <GlobalStyle />
            <Router/>
            <ReactQueryDevtools initialIsOpen={true}/>
        </>
    );
}
```
![[Pasted image 20231211195204.png]]
```typescript
    const {isLoading: infoLoading, data: infoData, } = useQuery<Info>(["info",coinId], () => fetchCoinInfo(coinId));
    const {isLoading: tickersLoading, data: tickersData, } = useQuery<Price>(["tickers",coinId], () => fetchCoinTickers(coinId));

```

## [APEXCHARTS](https://apexcharts.com/)

```typescript
data?.map(price => parseFloat(price.close)) as number[]
```
- as number[]
	- 결과가 숫자 배열이 될것으로 예상함을 나타내는 유형 주장이다.
	- 배열이 필요한 컨텍스트에서 이 결과를 사용하려고 하면 런타임 에러가 날수 있음
		- 결과가 undifine인 경우 undefine으로 이어질수 있다.
```typescript
data?.map(price => parseFloat(price.close)) ?? []
```
- ?? []
	- 결과가 null or undefine 이라면 null 병합 연산자(??) 를 활용해 기본값 [] 을 제공한다.
	- 이 방법이 확실하게 배열을 리턴받는다고 보장이 되기 때문에 더 안전함.
	- ??
		- nullish 병합 연산자

## [React helmet](https://www.npmjs.com/package/react-helmet)

- Component
	- 무엇을 render하던 그게 문서의 head로 가는것