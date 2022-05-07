# React Native 화면 변경 시 함수 호출

react native에서는 탭 네비게이터의 특정 화면을 렌더링할 때, API 혹은 함수를 호출할 수 있다. 

1. `focus` 이벤트 리스너로 이벤트를 수신한다.
2. `useFocusEffect` 를 사용한다.
3. `useIsFocused` 를 사용한다.



### focus 이벤트  사용

`navigation`을 import하고, `addListener` 이벤트를 통해 화면 진입 시 함수를 호출하거나 api 통신을 불러올 수 있다. `unmount` 시 사용해야할 함수가 있다면 return 뒤에 작성하면 된다.

```javascript
import * as React from 'react';
import { View } from 'react-native';

function ProfileScreen({ navigation }) {
  React.useEffect(() => {
    const unsubscribe = navigation.addListener('focus', () => {
      // The screen is focused
      // Call any action
    });

    // Return the function to unsubscribe from the event so it gets removed on unmount
    return unsubscribe;
  }, [navigation]);

  return <View />;
}
```



### useFocusEffect 사용

화면에 포커스가 될 때, 함수 혹은 api를 호출하고, 화면을 나갈 때, 실행할 코드를 작성할 수 있다.

 ```javascript
 import { useFocusEffect } from '@react-navigation/native';
 
 function Profile({ userId }) {
   const [user, setUser] = React.useState(null);
 
   useFocusEffect(
     React.useCallback(() => {
       const unsubscribe = API.subscribe(userId, user => setUser(data));
 
       return () => unsubscribe();
     }, [userId])
   );
 
   return <ProfileContent user={user} />;
 }
 ```



### useIsFocused 사용

`useIsFocuseed`는 화면에 초점을 맞추고, 초점을 해제할 때 특정 코드가 다시 렌더링되도록 한다. 화면의 특정 구성 요소를 다시 렌더링해야하는 경우에 주로 사용한다.

```javascript
import * as React from 'react';
import { Text } from 'react-native';
import { useIsFocused } from '@react-navigation/native';

function Profile() {
  // This hook returns `true` if the screen is focused, `false` otherwise
  const isFocused = useIsFocused();

  return <Text>{isFocused ? 'focused' : 'unfocused'}</Text>;
}
```



### 코드 적용하기

경매 물품을 등록하는 로직을 구현하였는데, input 창에 이전의 글들이 남아있어서 `Focus`를 사용하여 화면 진입 시 input 창의 value 값을 모두 지워버렸다. 하지만 진입 시 지우게 되면 매끄럽지 않게 진행되기 때문에  `focus` 이벤트에서 return 이후에 코드를 작성하여 화면을 나갈 때, 특정 코드를 실행시키려고 했다. 그런데, `return` 이후의 코드가 실행되지 않는 문제점이 있었다. 그래서 공식 문서를 찾아본 결과 다른 방법이 있다는 것을 알게 되었다.  `useFocusEffect`를 사용하여 return 이후에 `form`과 `value` 값을 모두 리셋시켰는데, 잘 동작되었고, 화면 전환도 매우 매끄럽게 구현할 수 있었다.

```javascript
import { useNavigation, useFocusEffect } from "@react-navigation/native";

useFocusEffect(
    React.useCallback(() => {
      return () => {
        setImgForm([]);
        setForm((prevState: any) => ({
          form: {
            title: "",
            content: "",
            startPrice: "",
            startTime: "",
            endTime: "",
            auctionType: "LIVE",
            itemCategories: "디지털기기",
          },
        }));
        setValue({
          title: "",
          startPrice: "",
          content: "",
        });
        setSelect(true);
      };
    }, []),
  );
```

