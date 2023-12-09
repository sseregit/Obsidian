## Typescript

- stringly-typed 언어
	-  프로그래밍 언어가 작동하기 전에 type 을 확인한다.

## [Type Scirpt 적용하기](https://create-react-app.dev/docs/adding-typescript/#installation)

- 확장자
	- typescript .ts
	- typescript + React .tsx

- npm start시 자동으로 tsconfig.json이 생성되지 않을경우
```
npx tsc --init
```

- 명령어를 활용해 수동으로 tsconfig.json을 생성한다.
```typescript
{
  "compilerOptions": {
     "jsx": "react-jsx",
  }
}
```
- *"jsx": "react-jsx*를 적어주면 된다.

```typescript
const root = ReactDOM.createRoot(document.getElementById('root') as HTMLElement);
```
- 해당 코드가 에러가 나는데 *as HTMLElement*를 추가하면 된다.

## Typing the Props

- interface
	- Object shape(객체 모양)을 TypeScript에게 설명해주는 개념

```typescript
interface CircleProps {
    bgColor: string;
}

function Circle({bgColor}: CircleProps) {
    return <Container bgColor={bgColor}/>
}
```
- Component에 interface를 적용하는법

```typescript
interface ContainerProps {
    bgColor: string;
}

const Container = styled.div<ContainerProps>`
    background-color: ${props=>props.bgColor};
  width: 200px;
  height: 200px;
  border-radius: 100px;
`;
```
- styled-components에 interface를 적용하는법

## Optional Props

```typescript
interface CircleProps {
    bgColor: string;
    borderColor?: string;
}
```
- ? 를 활용해 Optional로 활용한다

```typescript
return <Container bgColor={bgColor} borderColor={borderColor ?? bgColor}/>
```
- Optional 옵션의 필드를 전달할때 받는쪽이 required 옵션의 필드라면 default값을 줘야 전달할수있다.
```typescript

const requiredFiled = {optionalField ?? defaultField}

```

## useState to Typescript

```typescript
    const [value, setValue] = useState<number|string>(0);
    setValue(2);
    setValue("hello");

```
- 제네릭을 사용해 여러타입을 지정할수 있다.
- default value를 지정하면 typescript는 해당 타입으로 타입을 지정한다.

## Forms to Typescript

```typescript
function App() {
    const [value, setValue] = useState("");
    const onChange = (event: React.FormEvent<HTMLInputElement>) => {
        const {currentTarget: {value}} = event;
        setValue(value);
    }
    const onSubmit = (event: React.FormEvent<HTMLFormElement>) => {
        event.preventDefault();
        console.log("hello", value);
    }
    return (
        <div>
            <form onSubmit={onSubmit}>
                <input onChange={onChange} value={value} type={"text"} placeholder={"username"}/>
                <button>Log in</button>
            </form>
        </div>
    );
}

```

## Theme to Typescript

