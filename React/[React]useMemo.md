# useMemo()

### 리렌더링

React에서 컴포넌트의 렌더링은 수시로 발생할 수 있다. state가 업데이트되거나 부모 컴포넌트가 렌더링 되었을 때, 혹은 props가 업데이트 되었을 때 등은 리렌더링을 발생하게 한다. 빈번한 함수 호출, 리렌더링을 막기 위해 useMemo()를 사용할 수 있다.

</br>

</br>

 ### useMemo()

Memo : memoized, 이전에 계산한 값 재사용

리액트에서 컴포넌트가 리렌더링 될 때, 불필요한 함수가 실행되거나 리렌더링 되면 자원이 낭비되고 성능도 저하되는 문제가 발생한다. useMemo는 dependency array 값에 변화가 없다면 이전에 연산된 값을 리턴하여 불필요한 연산을 막아 성능을 최적화할 수 있다.

```javascript
const count = useMemo(() => countActiveUsers(users), [users]);
```

useMemo의 첫번째 파라미터에는 어떻게 연산할지 정의하는 함수를 넣어주면 되고, 두번째 파라미터에는 deps 배열을 넣어주면 되는데, 이 배열 안에 넣은 내용이 바뀌면 우리가 등록한 함수를 호출해서 값을 연산해주고, 만약에 내용이 바뀌지 않았다면 이전에 연산한 값을 재사용하게 된다.

</br>

</br>

### 주의할 점

무분별하게 사용하지 않아야 한다. 값을 재사용하기 위해 메모리를 소비하여 저장하는 것이기 때문에 너무 과하게 많이 사용하면 오히려 성능 저하를 일으킬 수 있다. 또한 코드가 복잡해질 수 있고, 코드 리팩토링이나 유지보수가 어려워질 수 있다. 그러므로 곡 필요한 경우에만 사용해야 한다.

</br>

</br>

### 전체코드

```javascript
import React, { useRef, useState } from 'react';
import UserList from './UserList';
import CreateUser from './CreateUser';

function countActiveUsers(users) {
  console.log('활성 사용자 수를 세는중...');
  return users.filter(user => user.active).length;
}

function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: ''
  });
    
  const { username, email } = inputs;
    
  const onChange = e => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value
    });
  };
    
  const [users, setUsers] = useState([
    {
      id: 1,
      username: 'velopert',
      email: 'public.velopert@gmail.com',
      active: true
    },
    {
      id: 2,
      username: 'tester',
      email: 'tester@example.com',
      active: false
    },
    {
      id: 3,
      username: 'liz',
      email: 'liz@example.com',
      active: false
    }
  ]);

  const nextId = useRef(4);
    
  const onCreate = () => {
    const user = {
      id: nextId.current,
      username,
      email
    };
    setUsers(users.concat(user));

    setInputs({
      username: '',
      email: ''
    });
    nextId.current += 1;
  };

  const onRemove = id => {
    setUsers(users.filter(user => user.id !== id));
  };
    
  const onToggle = id => {
    setUsers(
      users.map(user =>
        user.id === id ? { ...user, active: !user.active } : user
      )
    );
  };
    
  const count = countActiveUsers(users);
    
  return (
    <>
      <CreateUser
        username={username}
        email={email}
        onChange={onChange}
        onCreate={onCreate}
      />
      <UserList users={users} onRemove={onRemove} onToggle={onToggle} />
      <div>활성사용자 수 : {count}</div>
    </>
  );
}

export default App;
```

