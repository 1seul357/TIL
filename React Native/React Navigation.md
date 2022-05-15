# React Navigation

### ✈ React Navigation

웹 브라우저에서는 `<a>` 태그를 통해 다른 페이지로 연결할 수 있지만 React Native는 웹 브라우저처럼 히스토리 스택이 기본적으로 되어 있지 않다. React Native에서는 stack navigator를 통해 화면을 전환하고, 탐색 기록을 관리할 수 있다. 사용자가 상호작용할 때, 앱이 탐색 스택에서 항목을 푸시하고, 팝하면서 사용자에게는 다른 화면이 표시된다.



### Native stack navigator library

### 01. Install

```javascript
npm install @react-navigation/native-stack
```



### 02. CreateStackNavigator

Screen 및 Navigator라는 두 가지 속성이 포함 된 객체를 반환하는 함수이다. 둘 다 Navigator를 구성하는데 사용되는 React 구성 요소이며 경로에 대한 구성을 정의하기 위해 포함해야 한다.

```javascript
import * as React from 'react';
import { View, Text } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';

function HomeScreen() {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Home Screen</Text>
    </View>
  );
}

const Stack = createNativeStackNavigator();

function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen
          name="Home"
          component={HomeScreen}
          options={{ title: 'Overview' }}
        />
        <Stack.Screen name="Detail" component={Detail} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

export default App;
```



### 03. 기본 개념들

- `Stack.Navigator` 는 `Stack.Screen` 구성 요소를 사용하여 콘텐츠를 렌더링하는 구성요소이다.

- `name`은 경로 이름을 나타낸다.

- `component`는 경로에 렌더링할 구성 요소를 지정한다.

- `options`를 통해 `headerTitle`을 설정할 수 있다.

  ```javascript
  <Stack.Screen
      name="detail"
      component={DetailContainer}
      options={{
           headerTitleAlign: "center",
           headerTitle: (props) => (
               <NavigatorTitle
                   title={"물품 상세 정보"}
               	 style={styles.navigatorTitle}
  			/>
           )
  	}}
  />
  ```

- 스택의 초기 경로를 지정하는 방법

  ```javascript
  <Stack.Navigator initialRouteName="Home">
  ```

  

### 경로에 매개변수 전달

- `navigation.navigate` 함수의 두 번째 `params` 전달

- 화면 전환 후 `route.params` 통해 매개변수 가져오기

- 관련 코드

  ```javascript
  function HomeScreen({ navigation }) {
    return (
      <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
        <Text>Home Screen</Text>
        <Button
          title="Go to Details"
          onPress={() => {
            /* 1. Navigate to the Details route with params */
            navigation.navigate('Details', {
              itemId: 86,
              otherParam: 'anything you want here',
            });
          }}
        />
      </View>
    );
  }
  
  function DetailsScreen({ route, navigation }) {
    /* 2. Get the param */
    const { itemId, otherParam } = route.params;
    return (
      <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
        <Text>Details Screen</Text>
        <Text>itemId: {JSON.stringify(itemId)}</Text>
        <Text>otherParam: {JSON.stringify(otherParam)}</Text>
        <Button
          title="Go to Details... again"
          onPress={() =>
            navigation.push('Details', {
              itemId: Math.floor(Math.random() * 100),
            })
          }
        />
        <Button title="Go to Home" onPress={() => navigation.navigate('Home')} />
        <Button title="Go back" onPress={() => navigation.goBack()} />
      </View>
    );
  }
  ```

  

### 컴포넌트에 Props 전달

- `childeren`

  > component로 작성하는 것이 아니라 childeren을 통해 전달할 요소들을 넘겨주면 된다.

  ```javascript
  <Stack.Screen 
  	name={`Home`} 
  	children={({navigation})=>
          <Home name={name} setName={setName} navigation={navigation} />
  	}
  />
  ```

- `props`

  > props => 를 통해 데이터를 전달할 수 있다.

```javascript
<Stack.Screen name="Home">
  {props => <HomeScreen {...props} extraData={someData} />}
</Stack.Screen>
```



### 화면 간 이동

```javascript
import * as React from 'react';
import { Button, View, Text } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';

function HomeScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Home Screen</Text>
      <Button
        title="Go to Details"
        onPress={() => navigation.navigate('Details')}
      />
    </View>
  );
}
```

```javascript
function DetailsScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Details Screen</Text>
      <Button
        title="Go to Details... again"
        onPress={() => navigation.push('Details')}
      />
      <Button title="Go to Home" onPress={() => navigation.navigate('Home')} />
      <Button title="Go back" onPress={() => navigation.goBack()} />
      <Button
        title="Go back to first screen in stack"
        onPress={() => navigation.popToTop()}
      />
    </View>
  );
}
```

- 기본 Stack 탐색기에서 헤더는 화면에서 돌아갈 수 있는 경우, 자동으로 뒤로가기 버튼을 포함한다. `navigation.goBack()` 을 사용자가 누르면 바로 이전 화면으로 돌아갈 수 있다. `navigation.popToTop()` 는 스택의 첫 번째 화면으로 돌아갈 수 있게 한다.