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

