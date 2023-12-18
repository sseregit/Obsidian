## [Recoil](https://recoiljs.org/ko/)
- React JS에서 사용할 수 있는 state management library이다.
- global state
	- 어플리케이션 전체에서 공유되는 state
```typescript
npm install recoil
```

```typescript
import {RecoilRoot} from "recoil";

ReactDOM.render(
    <React.StrictMode>
        <RecoilRoot>
	        ...
	    </RecoilRoot>
	</React.StrictMode>,
document.getElementById('root')
)
```

- atom생성
```typescript
import {atom} from "recoil";


export const isDarkAtom = atom({
    key:"isDark",
    default: false,
})
```

- atom 호출
```typescript
function App() {
    const isDark = useRecoilValue(isDarkAtom);
    return (
        <>
            <ThemeProvider theme={isDark ? darkTheme : lightTheme}>
				...
            </ThemeProvider>
        </>
    );
}

```

- atom 수정
```typescript
function Coins() {
    const setDarkAtom = useSetRecoilState(isDarkAtom);
    const toggleDarkAtom = () => setDarkAtom(prev => !prev);
fetchCoins);
    return (
        <Container>
            <Header>
                <Title>코인</Title>
                <button onClick={toggleDarkAtom}>Toggle Mode</button>
            </Header>
        </Container>

    )
}
```
- useSetRecilState
	- useState의 setFuntion과 같은 역할을 한다.

## [React Hook Form](https://react-hook-form.com/)

```typescript
npm install react-hook-form
```

- useForm
```typescript
function ToDoList() {
    const { register, watch, handleSubmit, formState } = useForm();
    const onValid = (data) => ...;
    console.log(register("toDo"));
	    return (
        <div>
            <form onSubmit={handleSubmit(onValid)}>
                <input {...register("toDo", 
                {required: true, minLength: 10})} />
                <input {...register("toDo", 
                {required: "error Message", minLength: {
                        value: 5,
                        message: "Your password is too short."
                    }})} />
                <button>Add</button>
            </form>
        </div>
    );

}
```
- register
	- 넣은 문자가 name이 되고
	- onBlur 와 onChange를 가지고 있는 오브젝트가 된다.
	- ES6 문법을 활용해서 한번에 넣어줄수 있음
	- 기존에 활용하던 userState, value, onChange 모든걸 대체할수 있다.
	- option
		- validation 처리를 해준다. 
		- 자동 focus
		- value에 문자열을 입력시 formState.errors의 message가 된다.
		- value가 필요한 경우 value와 message의 object를 보낼수 있다.
- watch
	- form의 입력값을 추척할 수 있다.
		- 하나의 input이 아닌 form안에 있는 모든 input값을 추척한다.
- handleSubmit
	- onValid **(필수)**
		- 데이터가 유효할 때 호출되는 함수
		- form data를 인자로 받게 된다.
	- onInvalid
		- 데이터가 유효하지 않을 때 호출되는 함수
- formState
	- errors
		- 에러가 어떤 에러인지에 대한 정보가 담긴다.
