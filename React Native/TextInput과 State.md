# TextInput과 State

### TextInput

```javascript
import React, { Component } from 'react';
import { StyleSheet, View, Text, TextInput } from 'react-native';

class AuthForm extends Component {
    
    state = {
        myTextInput: 'asdf'
    }
    
    render () {
        return (
            <View>
            	<TextInput
            		value={this.state.myTextInput}
    				authCapitalize={'none'}
    				keyboardType={'email-address'}
    				style={styles.input}
    				placeholder="이메일 주소"
    				placeholderTextColor='#ddd'
            	/>
            </View>
        )
    }
}

const styles = StyleSheet.create({
    input : {
        width: '100%'
        borderBottomWidth: 1,
        fontSize: 17,
        padding: 5,
        marginTop: 30
    }
});

export default AuthForm;
```

- `authCapitalize` : 첫 글자 대문자로 만드는 것
- `keyboardType` : 키보드 타입 지정



### State

재사용 컴포넌트는 알맹이는 없고, 껍데기만 있는 것이다. 아래 코드는 style 컴포넌트를 만들고, 재사용하는 예이다. `props` 구성 요소를 제어하는 두 가지 유형의 데이터가 있다. `state`와 `props`인데 부모에 의해 설정되고 구성 요소가 유지되는 동안 고정된다. 데이터가 변경되는 경우 `state`를 사용해야 한다. `state`는 일반적으로 생성자에서 초기화 한 다음에 변경하고 싶을 때 `setState` 를 호출해야 한다.  

```javascript
import React from 'react';
import { StyleSheet, TextInput } from 'react-native';

const input = (props) => {
    let template = null;
    switch(props.type) {
        case "textinput":
            template = 
            <TextInput
                {...props}
                style={styles.input}
            />
        break:
        case "textinputRevised":
            template = 
            <TextInput
                {...props}
                style={styles.inputRevised}
            />
        break:
        default:
    		return template
	}
	return template
}
    
const styles = StyleSheet.create({
    input: {
        width: '100%'
        borderBottomWidth: 1,
        fontSize: 17,
        padding: 5,
        marginTop: 30
    },
    inputRevised: {
        width: '100%'
        borderBottomWidth: 3,
        fontSize: 17,
        padding: 5,
        marginTop: 30
    }
});

export default input;
```

```javascript
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 *
 * @format
 * @flow
 */
import React, { Component } from 'react';
import { StyleSheet, View, Text, TextInput, Button, Platform } from 'react-native';
import Input from '../../utils/forms/input';
import ValidationRules from '../../utils/forms/validationRules';

import { connect } from 'react-redux';
import { signIn, signUp } from '../../store/actions/user_actions';
import { bindActionCreators } from 'redux';
import { setTokens } from '../../utils/misc';

class AuthForm extends Component {

  state = {
      type: '로그인', // 로그인 / 등록
      action: '로그인', // 로그인 / 등록
      actionMode: '회원가입', // 회원가입 / 로그인 화면으로
      hasErrors: false,
      form: {
        email: {
          value: "",
          type: "textinput",
          rules: {
            isRequired: true,
            isEmail: true
          },
          valid: false
        },
        password: {
          value: "",
          type: "textinput",
          rules: {
            isRequired: true,
            minLength: 6
          },
          valid: false
        },
        confirmPassword: {
          value: "",
          type: "textinput",
          rules: {
            confirmPassword: 'password'
          },
          valid: false
        }
      }
  }

  updateInput = (name, value) => {
    this.setState({
      hasErrors: false
    })

    let formCopy = this.state.form;
    formCopy[name].value = value;

    // rules
    let rules = formCopy[name].rules;
    let valid = ValidationRules(value, rules, formCopy);
    formCopy[name].valid = valid;

    this.setState({
      form: formCopy
    })

    // console.warn(this.state.form)
  }

  confirmPassword = () => (
    this.state.type != '로그인' ?
      <Input
        value={this.state.form.confirmPassword.value}
        type={this.state.form.confirmPassword.type}
        secureTextEntry={true}
        placeholder="비밀번호 재입력"
        placeholderTextColor='#ddd'
        onChangeText={value=>this.updateInput("confirmPassword", value)}
      />
    : null
  )

  formHasErrors = () => (
    this.state.hasErrors ?
      <View style={styles.errorContainer}>
        <Text style={styles.errorLabel}>
          엇! 로그인 정보를 다시 확인해주세요~
        </Text>
      </View>
    : null
  )

  changeForm = () => {
    const type = this.state.type;

    this.setState({
      type: type === '로그인' ? '등록' : '로그인',
      action: type === '로그인' ? '등록' : '로그인',
      actionMode: type === '로그인' ? '로그인 화면으로' : '회원가입'
    })
  }

  submitUser = () => {
    // Init.
    let isFormValid = true;
    let submittedForm = {};
    const formCopy = this.state.form;

    for (let key in formCopy) {
      if (this.state.type === '로그인') {
        if (key !== 'confirmPassword') {
          isFormValid = isFormValid && formCopy[key].valid;
          submittedForm[key] = formCopy[key].value;
        }
      } else {
        isFormValid = isFormValid && formCopy[key].valid;
        submittedForm[key] = formCopy[key].value;
      }
    }

    if (isFormValid) {
      if (this.state.type === '로그인') {
        this.props.signIn(submittedForm).then(()=>{
          this.manageAccess();
        })
      } else {
        this.props.signUp(submittedForm).then(()=>{
          this.manageAccess();
        })
      }
    } else {
      this.setState({
        hasErrors: true
      })
    }
  }

  manageAccess = () => {
    if (!this.props.User.auth.userId) {
      this.setState({hasErrors: true})
    } else {
      setTokens(this.props.User.auth, ()=>{
        this.setState({hasErrors: false});
        //this.props.goWithoutLogin();
        this.props.navigation.push("AppTabComponent")
      })
    }
  }

  render () {
    return (
      <View>
        <Input
          value={this.state.form.email.value}
          type={this.state.form.email.type}
          autoCapitalize={'none'}
          keyboardType={'email-address'}
          placeholder="이메일 주소"
          placeholderTextColor='#ddd'
          onChangeText={value=>this.updateInput("email", value)}
        />

        <Input
            value={this.state.form.password.value}
            type={this.state.form.password.type}
            secureTextEntry={true}
            placeholder="비밀번호"
            placeholderTextColor='#ddd'
            onChangeText={value=>this.updateInput("password", value)}
        />

        {this.confirmPassword()}
        {this.formHasErrors()}

        <View style={{marginTop: 40}}>
          <View style={styles.button}>
            <Button
              title={this.state.action}
              color="#48567f"
              onPress={this.submitUser}
            />
          </View>

          <View style={styles.button}>
            <Button
              title={this.state.actionMode}
              color="#48567f"
              onPress={this.changeForm}
            />
          </View>

          <View style={styles.button}>
            <Button
              title="비회원 로그인"
              color="#48567f"
              onPress={()=>this.props.goWithoutLogin()}
            />
          </View>                    
        </View>
      </View>
    )
  }
}

const styles = StyleSheet.create({
  errorContainer: {
    marginBottom: 10,
    marginTop: 30,
    padding: 20,
    backgroundColor: '#ee3344'
  },
  errorLabel: {
    color: '#fff',
    fontSize: 15,
    fontWeight: 'bold',
    textAlignVertical: 'center',
    textAlign: 'center'
  },
  button: {
    ...Platform.select({
      ios: {
        marginTop: 15
      },
      android: {
        marginTop: 15,
        marginBottom: 10
      }
    })
  }
});

function mapStateToProps(state) {
  return {
    User: state.User
  }
}

function mapDispatchToProps(dispatch) {
  return bindActionCreators({signIn, signUp}, dispatch);
}

export default connect(mapStateToProps, mapDispatchToProps)(AuthForm);

```

```javascript
goWithoutLogin = () => {
    this.props.navigation.navigate("AppTabComponent")
}
```

- `actionMode` : 버튼의 title로 쓰일 String 값
- `hasErrors` : 에러 발생 시 true 반환해서 alert 띄우기
- `onChangeText={value=>this.updateInput("email", value)}` : `value` 변경 시 `updateInput` 함수 실행되는데 인자로 `email`과 `value` 전달
- `isRequired` : 꼭 필요한 값
- `isEmail` : email 형식이어야 함