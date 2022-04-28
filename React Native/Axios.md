### axios

```javascript
export funciont signUp(data) {
    
    const request = axios({
        method: "post",
        url: SIGNUP,
        data: {
            email: data.eamil,
            password: data.password,
            returnSecureToken: true
        },
        header: {
            "Content-Type": "application/json"
        }
    }).then(response=>{
        return response.data
    }).catch(err=>{
        alert("에러 발생!")
        return false
    })
    
    
    return {
        type: SIGN_IN,
        payload: request
    }
}
```

