# React Axios 활용하기

```javascript
import axios from 'axios';


export const instance = axios.create({
  baseURL: process.env.REACT_APP_URL,
  headers: {
    'Content-type': 'application/json',
    Authorization: `Bearer ${localStorage.getItem('access_token')}`,
  }
});
```

- instance 객체를 만들어서 axios를 사용했는데, 서버로 데이터를 보낼 때 headers에 access_token이 null 값으로 간다는 것을 알게 되었다. 새로고침을 하면 토큰이 서버로 잘 가는데, 새로고침을 하지 않으면 null 값이 가는 것을 알게 되고, 해결방법을 찾았다.



#### interceptor

request와 response 이벤트를 interceptor 할 수 있는데, request 시에는 서버로 요청보내기 바로 전의 정보를 interceptor 하며, response 시에는 서버에서 리턴받은 데이터를 프론트로 리턴하기 전에 interceptor 하는 것이다.

```javascript
export const setApiHeaders = () => {
  instance.interceptors.request.use( 
  config => {
    config.headers["Authorization"] = `Bearer ${
      localStorage.getItem("access_token")
    }`
    return config;
  },
  err => {
    return Promise.reject(err);
  }
)};
```

```javascript
const result = await googleLogin(data, response.tokenId);
    if (result.status === 200) {
      try {
        setIsLoginState(true);
        setUserInfoState(result.user.member_seq);
        setApiHeaders();
        if (result.user.isSurvey === false) {
          navigate("/survey");
        } else {
          navigate("/category");
        }
      }
      catch {
        window.location.reload();
      }
    } else {
      Alert("Please check your information.");
    }
```

- headers에 토큰 값을 넣어서 api 요청을 보내야 할 때, request를 interceptor 하여 config.headers에 토큰을 추가하면 새로고침을 하지 않더라도 로그인 후 토큰 값이 서버로 보내지게 된다.

  > 로그인 후 설문조사 or 메인 페이지로 이동하기 전에 interceptor 사용

