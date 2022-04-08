# Recoil-persist와 useRecoilState

### Recoil-persist

페이지를 새로고침할 때 데이터가 삭제되는 것을 방지하기 위해 Recoil-persist를 사용할 수 있다. 해당 state는 localStorage에 저장된다. 

- 설치 : `npm instll recoil-persist`
- 코드 추가 : `import { recoilPersist } from 'recoil-persist'`
- 상태 유지할 state에 `effects_UNSTABLE: [persistAtom],` 추가

```javascript
import { atom } from 'recoil';
import { recoilPersist } from 'recoil-persist'

const { persistAtom } = recoilPersist()

/* Sample code */
// export const sampleState = atom({
//   key: 'exState', // unique ID (with respect to other atoms/selectors)
//   default: '', // default value (aka initial value)
// });

/*
Atom : 상태. 해당 아톰을 참고하고 있는 컴포넌트를 리렌더링함
*/

export const userInfoState = atom({
  key: 'userInfoState',
  default: [],
  effects_UNSTABLE: [persistAtom],
});


export const isLoginState = atom({
  key: 'isLoginState',
  default: false,
  effects_UNSTABLE: [persistAtom],
});

```



### useRecoilState

첫 번째 요소(tempF)가 상태의 값이며, 두 번째 요소(setTempF)가 호출되었을 때 주어진 값을 업데이트하는 setter 함수인 튜플을 리턴한다. 컴포넌트가 상태를 읽고, 쓰려고 할 때 사용할 수 있다.

```javascript
import {atom, selector, useRecoilState} from 'recoil';

const tempFahrenheit = atom({
  key: 'tempFahrenheit',
  default: 32,
});


function TempCelsius() {
  const [tempF, setTempF] = useRecoilState(tempFahrenheit);
}

```



### useRecoilValue

주어진 Recoil 상태의 값을 리턴한다. 컴포넌트가 상태를 읽을 때 사용할 수 있다.

```javascript
import {atom, selector, useRecoilValue} from 'recoil';

const namesState = atom({
  key: 'namesState',
  default: ['', 'Ella', 'Chris', '', 'Paul'],
});


function NameDisplay() {
  const names = useRecoilValue(namesState);
}
```



### useSetRecoilState

쓰기 가능한 Recoil 상태의 값을 업데이트하기 위한 setter 함수를 리턴한다. 컴포넌트가 상태를 쓸 때 사용할 수 있다.

```javascript
import {atom, useSetRecoilState} from 'recoil';

const namesState = atom({
  key: 'namesState',
  default: ['Ella', 'Chris', 'Paul'],
});

function FormContent({setNamesState}) {
  const [name, setName] = useState('');
  
  return (
    <>
      <input type="text" value={name} onChange={(e) => setName(e.target.value)} />
      <button onClick={() => setNamesState(names => [...names, name])}>Add Name</button>
    </>
)}

// This component will be rendered once when mounting
function Form() {
  const setNamesState = useSetRecoilState(namesState);
  
  return <FormContent setNamesState={setNamesState} />;
}

```

