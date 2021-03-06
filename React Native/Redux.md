# Redux

### ๐ป Redux

์ ํ๋ฆฌ์ผ์ด์ ์ํ (State)๋ฅผ ์ฉ์ดํ๊ฒ ๊ด๋ฆฌํ๊ธฐ ์ํ ํ๋ ์์ํฌ (์คํ ์์ค ์๋ฐ์คํฌ๋ฆฝํธ ๋ผ์ด๋ธ๋ฌ๋ฆฌ)

</br>
</br>

### Action

- ์ํ๋ฅผ ๋ณ๊ฒฝํ๊ธฐ ์ํด ๋ฐ์

- ๊ฐ์ฒด ํ์

  ```
  {
  	type: "EXAMPLE_TYPE"
  	payload: amount
  }
  ```

</br>
</br>

### Action Creator

- Action์ ์์ฑํ๋ ํจ์

- Action์ ๋ฐํํ๋ ํจ์

  ```
  const withdrawMoney = (param) => {
  	return {
  		type: WITHDRAW_MONEY,
  		payload: amount
  	}
  }
  ```

</br>
</br>

### dispatch

- Store์ ๋ด์ฅ ํจ์ ์ค ํ๋
- Reducer์๊ฒ ์ด๋ค action์ด ๋ฐ์ํ๋์ง ์๋ฆฌ๋ ํจ์
- dispatch(action), dispatch(ActionCreator(param))

</br>
</br>

### Store

- ํ๋์ App์ ๋จ ํ๋์ Store๋ง ์กด์ฌ
- state, Reducer ๋ฐ ๊ธฐํ ๋ด์ฅ ํจ์ ์กด์ฌ

</br>
</br>

### State

- ๋ฐ์ดํฐ ๋ฐ UI ์ํ ๋ฑ ์ดํ๋ฆฌ์ผ์ด์์ ์ ์งํ๊ธฐ ์ํ ์ ๋ณด
- state์ ๋ณ๊ฒฝ, View์ ๋ณ๊ฒฝ

</br>
</br>

### Reducer

- state์ ๋ณํ๋ฅผ ์ผ์ผํค๋ ํจ์
- Input : state, action
- output: state'

</br>
</br>

### Connect

- React Native ์ธ๊ณ๊ด๊ณผ  Redux ์ธ๊ณ๊ด์ ์ฐ๊ฒฐ ํจ์
- Store ๋ด state -> connect -> component ๋ด props
- state ๋ณ๊ฒฝ -> ์๋ก์ด component ์์ฑ
- Store๊ฐ ๊ฐ์ง state๋ฅผ ์ด๋ป๊ฒ props์ ์ฎ์์ง -> mapStateToProps
- Reducer์ Action์ ์๋ฆฌ๋ ํจ์ dispatch๋ฅผ ์ด๋ป๊ฒ props์ ์ฎ์์ง -> mapDispatchToProps -> connect (mapStateToProps, mapDispatchToProps)

</br>
</br>

### Redux์ 3์์น

- Single Source of Truth

  > ์ดํ๋ฆฌ์ผ์ด์์ ๋ชจ๋  state๋ ๋จ์ผ store์์ ๊ด๋ฆฌ

- State in Read-Only

  > state์ ๋ณ๊ฒฝ์ ๋ฐ๋์ action์ ํตํด์ ๊ฐ๋ฅ

- Changes are made with Pure Functions

  > Reducer๋ ์์ ํจ์๋ก ์ ์
  >
  > - ์ธ์ ๋ณ๊ฒฝ X
  > - API ํธ์ถ X
  > - ๋คํธ์ํฌ ์์ฒญ X
  > - ์์ํจ์๊ฐ ์๋ ํจ์์ ํธ์ถ X
