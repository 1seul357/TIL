#### vue에서 사용자 정보 출력하기

django에서는 request.user를 통해 현재 user의 username을 알 수 있었고, 해당 영화를 찜한 유저 목록에 사용자가 있는지 없는지 체크하는 것도 쉽게 할 수 있었다.

Vue에서는 다른 방법을 통해 수행해야 한다.

```vue
<script>
...
created: function () {
    if (localStorage.getItem('jwt')) {
      const token = localStorage.getItem('jwt')
      const decoded = jwt_decode(token)
      // console.log(decoded)
      this.userpk = decoded.user_id
      this.getMovie(this.$route.params.movie_pk)
    } else {
      this.$router.push({name: 'Login'})
    }
  }
</script>
```

- 먼저 jwt_decode를 설치한다.
- 그리고 import jwt_decode from 'jwt-decode';를 작성한다.
- localStorage에서 jwt를 꺼내서 token 변수에 저장하고, 이것을 decoding 한다.
- 콘솔을 통해 출력되는 값을 확인해보면 user_id와 email, username 등등을 확인할 수 있다.
- 필요한 정보를 변수에 저장해서 사용하면 된다.