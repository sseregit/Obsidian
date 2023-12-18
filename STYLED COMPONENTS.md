### Styled Components

```javascript
import styled from "styled-components";  
  
const Father = styled.div`  
display: flex;  
`;  
  
const BoxOne = styled.div`  
background-color: teal;  
width: 100px;  
height: 100px;  
`;  
  
const BoxTwo = styled.div`  
background-color: tomato;  
width: 100px;  
height: 100px;  
`;  
  
function App() {  
return (  
<Father>  
	<BoxOne />  
	<BoxTwo />  
</Father>  
);  
}
```

- 'back tick' 안에 css코드를 넣는다.

## props를 활용하는법

```javascript
const Box = styled.div`  
	background-color: ${(props => props.bgColor)};  
	width: 100px;  
	height: 100px;  
`;

function App() {  
return (  
	<Father>  
		<Box bgColor="teal" />  
		<Circle bgColor="tomato" />  
	</Father>  
);  
}
```

## 컴포넌트를 확장하는법

```javascript
const Box = styled.div`
  background-color: ${(props => props.bgColor)}; 
  width: 100px; 
  height: 100px;
`;

const Circle = styled(Box)`
  border-radius: 50px;
`;

function App() {  
return (  
	<Father>  
		<Box bgColor="teal" />  
		<Circle bgColor="tomato" />  
	</Father>  
);  
}

```

## as를 활용한 tag 변경

```javascript
const Btn = styled.button`
  color: white;
  background-color: tomato;
  border: 0;
  border-radius: 15px;
`;

function App() {
  return (
      <Father>
          <Btn>Log in</Btn>
          <Btn as="a" href="/">Log in</Btn>
      </Father>
  );
}

```

- as에 적힌 태그로 변경되면서 css는 유지 된다.

## tag의 attributes 추가하는법

```javascript
const Input = styled.input.attrs({
    required: true
})`
  background-color: tomato;
`;
```

## animation

```javascript
const rotationAnimation = keyframes`
  0% {
    transform: rotate(0deg);
    border-radius: 0px;
  }
  50% {
    transform: rotate(360deg);
    border-radius: 100px;
  }
  100%{
    transform: rotate(360deg);
    border-radius: 0px;
  }
`;

const Box = styled.div`
  height: 200px;
  width: 200px;
  background-color: tomato;
  display: flex;
  justify-content: center;
  align-items: center;
  animation: ${rotationAnimation} 1s linear infinite;
  }
`;

```

- keyframes로 animation을 전달할수 있다

## Pesudo Selectors To Tag

```javascript
const Box = styled.div`
  span {
    font-size: 36px;
    &:hover {
      font-size: 40px;
    }
    &:active {
      opacity: 0;
    }
  }
`;
```

## Pesudo Selectors To Component

```javascript
const Emoji = styled.span`
  font-size:36px;
`;

const Box = styled.div`
  ${Emoji}:hover {
      font-size: 40px;
    }
  }
`;
```

- 해당 장점은 as를 활용해 tag를 변경해도 컴포넌트 기준이므로 적용이 된다.

## Themes

- 기본적으로 모든 색상들을 가지고 있는 *object* 이다.
- 색상을 변경할때 theme만 바꿔주면 된다.

```javascript
import {ThemeProvider} from "styled-components";

const root = ReactDOM.createRoot(document.getElementById('root'));

const darkTheme = {
    textColor: "whitesmoke",
    backgroundColor: "#111",
}

const lightTheme = {
    textColor: "#111",
    backgroundColor: "whitesmoke",
}

root.render(
    <React.StrictMode>
        <ThemeProvider theme={darkTheme}>
            <App/>
        </ThemeProvider>
    </React.StrictMode>
);
```

- ThemeProvider 를 추가하고 theme props를 추가한다.

```javascript
const Title = styled.h1`
  color: ${props => props.theme.textColor}
`;

const Wrapper = styled.div`
  background-color: ${props => props.theme.backgroundColor};
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
`;

```

- 그후 ThemeProvider 내부에 있는 화면은 해당 theme props에 접근할수 있다.