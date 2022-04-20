# Screen

### 🖥 Screen

`Screen` 구성 요소는 내비게이터 내부 화면의 다양한 측면을 구성하는데 사용된다. `Screen`은 `createXNavigator `함수에서 반환된다.

```javascript
const Stack = createNativeStackNavigator();
```

`Navigator`를 만든 후 구성 요소의 자식으로 사용할 수 있다.

```javascript
<Stack.Navigator>
    <Stack.Screen name="Home" component={HomeScreen} />
    <Stack.Screen name="Profile" component={ProfileScreen} />
</Stack.Navigator>
```



### name

화면에 사용할 이름이다. 이 이름은 화면으로 이동하는데 사용된다.

```javascript
navigation.navigate('Profile');
```



### options

네비게이터에 화면이 표시되는 방식을 구성하는 옵션이다. 객체 또는 객체를 반환하는 함수를 사용할 수 있다.

```javascript
<Stack.Screen 
	name="Profile"
	component={ProfileScreen}
	options={{
             title: 'Awesome app',                  // 객체 반환
            }}
	}}
/>
```

```javascript
<Stack.Screen
    name="Profile"
    component={ProfileScreen}
    options={({ route, navigation }) => ({          // 함수 전달
      title: route.params.userId,
    })}
/>
```



### initialParams

화면에 사용할 초기 매개변수이다. 화면이 `initialRouteName`으로 사용되면 `initialParams`매개변수가 포함된다. 새 화면으로 이동하면 전달된 매개변수가 초기 매개변수와 병합된다.

```javascript
<Stack.Screen
	name="Details"
	component={DetailScreen}
	initialParams={{ itemId: 42 }}
/>
```



### getId

화면에 사용할 고유 ID를 반환하는 콜백이다. 경로 매개변수가 있는 객체를 수신한다.

```javascript
<Stack.Screen
	name="Profile"
	component={ProfileScreen}
	getId={({ params }) => params.userId}
/>
```

기본적으로 호출 `navigate('ScreenName', params)`하면 이름으로 화면을 식별하고, 해당 화면으로 이동한다. `getId`를 지정하고, `undefined`를 리턴하지 않으면 화면 이름과 반환된 ID로 화면이 식별된다. 



### component

화면에 렌더링할 React 구성요소이다.

```javascript
<Stack.Screen name="Profile" component={ProfileScreen} />
```



### getComponent

화면에 렌더링할 React 구성 요소를 반환하는 콜백이다.

```javascript
<Stack.Screen
	name="Profile"
	getComponent={() => require('./ProfileScreen').default}
/>
```



### childeren

화면에 사용할 React Element를 반환하는 렌더링 콜백이다.

```javascript
<Stack.Screen name="Profile">
    {(props) => <ProfileScreen {...props} />}
</Stack.Screen>
```

`component` 추가 props를 전달해야 하는 경우 prop 대신 이 접근 방식을 사용할 수 있다.



### navigationKey

화면의 선택적 키이다. 고유하지 않아도 되며 키가 변경되면 이 이름을 가진 기존 화면이 제거되거나 재설정된다.

```javascript
<Stack.Screen
	navigationKey={isSignedIn ? 'user' : 'guest'}
	name="Profile"
	component={ProfileScreen}
/>
```

