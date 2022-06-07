# Redux와 Firebase Data 연결하기

### 🎉 Redux와 Firebase Data 연결하기

```javascript
import { GET_DIARIES } from '../types';
import axios from 'axios';

export function getDiaries() {
    const request = axios({
        method: 'GET',
        url: ''
    }).then(response=>{
        const diaryData = [];
        for (let key in response.data) {
            if (response.data[key]) {
                diaryData.push({
                    ...response.data[key]
                })
            }
        }
        return diaryData;
    }).catch(err=> {
        alert('Get Failed!')
        return false;
    })
    return {
        type: GET_DIARIES,
        payload: request
    }
}
```

- axios 호출하고, 성공하면 diaryData 빈 배열로 선언하고 반복문을 돌려준다.
- response.data의 길이만큼 반복문을 돌리면서 diaryData 배열에 response.data 값을 푸시해준다.
- 반복문이 끝나면 diaryData를 리턴한다.

</br>

```javascript
// diary_reducer.js

import { GET_DIARIES } from '../types';

export default function (state={}, action) {
    switch(action.type) {
        case GET_DIARIES:
            return {
                ...state,
                documents: action.payload || false
            }
        default:
            return state
    }
}
```

```javascript
// index.js

/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 *
 * @format
 * @flow
 */
import React, { Component } from 'react';
import { StyleSheet, View, Text } from 'react-native';
import { connect } from 'react-redux';
import { getDiaries } from '../../store/actions/diary_actions';


class DiaryComponent extends Component {

  componentDidMount() {
  	this.props.dispatch(getDiaries())
  };

  render () {
    return (
      <View>
      </View>
    )
  }
}

function mapStateToProps(state) {
  return {
    Diaries: state.Diaries,
    User: state.User
  }
}

export default connect(mapStateToProps)(DiaryComponent);
```

- `Diaries` : 리액트 네이티브에서 쓰이는 props
- `state.Diaries` : 리덕스의 state 상태
- 리액트 네이티브에서 리덕스 사용하기 위해서는 connect 함수를 사용해야 한다.
- `componentDidMount()` : 컴포넌트가 마운트된 직후, 호출된다.
