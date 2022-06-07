# AsyncStorage

### 🎟 AsyncStorage

앱 전체에 적용되는 암호화되지 않은 비동기식 키-값 스토리지 시스템이다. LocalStorage 대신 사용할 수 있다. 

`AsyncStorage` 라이브러리 가져오기

```javascript
import { AsyncStorage } from 'react-native';
```

지속 데이터

```javascript
_storeData = async () => {
  try {
    await AsyncStorage.setItem(
      '@MySuperStore:key',
      'I like to save it.'
    );
  } catch (error) {
    // Error saving data
  }
};
```

데이터 가져오기

```javascript
_retrieveData = async () => {
  try {
    const value = await AsyncStorage.getItem('TASKS');
    if (value !== null) {
      // We have data!!
      console.log(value);
    }
  } catch (error) {
    // Error retrieving data
  }
};
```

</br>
</br>

### getItem()

`key`에 대한 항목을 가져오고 완료 시 콜백을 호출한다. `Promise` 개체를 반환한다.

</br>
</br>

### setItem()

`key` 값을 설정하고, 완료 시 콜백을 호출한다. `Promise` 개체를 반환한다.

</br>
</br>

### removeItem()

`key`에 대한 항목을 제거하고, 완료 시 콜백을 호출한다. `Promise` 개체를 반환한다.

</br>
</br>

### multiSet()

여러 key-value 쌍을 일괄적으로 저장한다. 

```javascript
export const setTokens = async (values, callBack) => {
    const firstPair = ["@winthiary_app@userId", values.userId]
    const secondPair = ["@winthidary_app@token", values.token]
    const thirdPair = ["@winthidary_app@refToken", values.refToken]
    try {
      await AsyncStorage.multiSet([firstPair, secondPair, thirdPair]).then(response=>{callBack()})
    } catch(e) {
      //save error
    }
  }
```

</br>
</br>

### multiGet()

`key` 입력 배열을 일괄로 가져올 수 있다.

```javascript
export const getTokens = async (callBack) => {

    let values
    try {
      values = await AsyncStorage.multiGet([
          '@winthiary_app@userId', 
          '@winthidary_app@token',
          '@winthidary_app@refToken'
        ]).then(values=>{
            callBack(values)
        })
    } catch(e) {
      // read error
    }
  
    // example console.log output:
    // [ ['@MyApp_user', 'myUserValue'], ['@MyApp_key', 'myKeyValue'] ]
  }
```



