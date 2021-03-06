# AsyncStorage

### π AsyncStorage

μ± μ μ²΄μ μ μ©λλ μνΈνλμ§ μμ λΉλκΈ°μ ν€-κ° μ€ν λ¦¬μ§ μμ€νμ΄λ€. LocalStorage λμ  μ¬μ©ν  μ μλ€. 

`AsyncStorage` λΌμ΄λΈλ¬λ¦¬ κ°μ Έμ€κΈ°

```javascript
import { AsyncStorage } from 'react-native';
```

μ§μ λ°μ΄ν°

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

λ°μ΄ν° κ°μ Έμ€κΈ°

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

`key`μ λν ν­λͺ©μ κ°μ Έμ€κ³  μλ£ μ μ½λ°±μ νΈμΆνλ€. `Promise` κ°μ²΄λ₯Ό λ°ννλ€.

</br>
</br>

### setItem()

`key` κ°μ μ€μ νκ³ , μλ£ μ μ½λ°±μ νΈμΆνλ€. `Promise` κ°μ²΄λ₯Ό λ°ννλ€.

</br>
</br>

### removeItem()

`key`μ λν ν­λͺ©μ μ κ±°νκ³ , μλ£ μ μ½λ°±μ νΈμΆνλ€. `Promise` κ°μ²΄λ₯Ό λ°ννλ€.

</br>
</br>

### multiSet()

μ¬λ¬ key-value μμ μΌκ΄μ μΌλ‘ μ μ₯νλ€. 

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

`key` μλ ₯ λ°°μ΄μ μΌκ΄λ‘ κ°μ Έμ¬ μ μλ€.

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



