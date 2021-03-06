# Screen

### π₯ Screen

`Screen` κ΅¬μ± μμλ λ΄λΉκ²μ΄ν° λ΄λΆ νλ©΄μ λ€μν μΈ‘λ©΄μ κ΅¬μ±νλλ° μ¬μ©λλ€. `Screen`μ `createXNavigator `ν¨μμμ λ°νλλ€.

```javascript
const Stack = createNativeStackNavigator();
```

`Navigator`λ₯Ό λ§λ  ν κ΅¬μ± μμμ μμμΌλ‘ μ¬μ©ν  μ μλ€.

```javascript
<Stack.Navigator>
    <Stack.Screen name="Home" component={HomeScreen} />
    <Stack.Screen name="Profile" component={ProfileScreen} />
</Stack.Navigator>
```

</br>
</br>

### name

νλ©΄μ μ¬μ©ν  μ΄λ¦μ΄λ€. μ΄ μ΄λ¦μ νλ©΄μΌλ‘ μ΄λνλλ° μ¬μ©λλ€.

```javascript
navigation.navigate('Profile');
```

</br>
</br>

### options

λ€λΉκ²μ΄ν°μ νλ©΄μ΄ νμλλ λ°©μμ κ΅¬μ±νλ μ΅μμ΄λ€. κ°μ²΄ λλ κ°μ²΄λ₯Ό λ°ννλ ν¨μλ₯Ό μ¬μ©ν  μ μλ€.

```javascript
<Stack.Screen 
	name="Profile"
	component={ProfileScreen}
	options={{
             title: 'Awesome app',                  // κ°μ²΄ λ°ν
            }}
	}}
/>
```

```javascript
<Stack.Screen
    name="Profile"
    component={ProfileScreen}
    options={({ route, navigation }) => ({          // ν¨μ μ λ¬
      title: route.params.userId,
    })}
/>
```

</br>
</br>

### initialParams

νλ©΄μ μ¬μ©ν  μ΄κΈ° λ§€κ°λ³μμ΄λ€. νλ©΄μ΄ `initialRouteName`μΌλ‘ μ¬μ©λλ©΄ `initialParams`λ§€κ°λ³μκ° ν¬ν¨λλ€. μ νλ©΄μΌλ‘ μ΄λνλ©΄ μ λ¬λ λ§€κ°λ³μκ° μ΄κΈ° λ§€κ°λ³μμ λ³ν©λλ€.

```javascript
<Stack.Screen
	name="Details"
	component={DetailScreen}
	initialParams={{ itemId: 42 }}
/>
```

</br>
</br>

### getId

νλ©΄μ μ¬μ©ν  κ³ μ  IDλ₯Ό λ°ννλ μ½λ°±μ΄λ€. κ²½λ‘ λ§€κ°λ³μκ° μλ κ°μ²΄λ₯Ό μμ νλ€.

```javascript
<Stack.Screen
	name="Profile"
	component={ProfileScreen}
	getId={({ params }) => params.userId}
/>
```

κΈ°λ³Έμ μΌλ‘ νΈμΆ `navigate('ScreenName', params)`νλ©΄ μ΄λ¦μΌλ‘ νλ©΄μ μλ³νκ³ , ν΄λΉ νλ©΄μΌλ‘ μ΄λνλ€. `getId`λ₯Ό μ§μ νκ³ , `undefined`λ₯Ό λ¦¬ν΄νμ§ μμΌλ©΄ νλ©΄ μ΄λ¦κ³Ό λ°νλ IDλ‘ νλ©΄μ΄ μλ³λλ€. 

</br>
</br>

### component

νλ©΄μ λ λλ§ν  React κ΅¬μ±μμμ΄λ€.

```javascript
<Stack.Screen name="Profile" component={ProfileScreen} />
```

</br>
</br>

### getComponent

νλ©΄μ λ λλ§ν  React κ΅¬μ± μμλ₯Ό λ°ννλ μ½λ°±μ΄λ€.

```javascript
<Stack.Screen
	name="Profile"
	getComponent={() => require('./ProfileScreen').default}
/>
```

</br>
</br>

### childeren

νλ©΄μ μ¬μ©ν  React Elementλ₯Ό λ°ννλ λ λλ§ μ½λ°±μ΄λ€.

```javascript
<Stack.Screen name="Profile">
    {(props) => <ProfileScreen {...props} />}
</Stack.Screen>
```

`component` μΆκ° propsλ₯Ό μ λ¬ν΄μΌ νλ κ²½μ° prop λμ  μ΄ μ κ·Ό λ°©μμ μ¬μ©ν  μ μλ€.

</br>
</br>

### navigationKey

νλ©΄μ μ νμ  ν€μ΄λ€. κ³ μ νμ§ μμλ λλ©° ν€κ° λ³κ²½λλ©΄ μ΄ μ΄λ¦μ κ°μ§ κΈ°μ‘΄ νλ©΄μ΄ μ κ±°λκ±°λ μ¬μ€μ λλ€.

```javascript
<Stack.Screen
	navigationKey={isSignedIn ? 'user' : 'guest'}
	name="Profile"
	component={ProfileScreen}
/>
```

