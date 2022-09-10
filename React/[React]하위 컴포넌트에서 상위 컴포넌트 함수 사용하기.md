# 하위 컴포넌트에서 상위 컴포넌트 함수 사용하기

```javascript
import React, { useEffect, useState } from 'react';
import InformationSurvey from 'components/accounts/survey/InformationSurvey';


const getInformation = (Info)=>{
    const allergyInformation = [1, 2, 3, 4, 5, 6, 7];
    const ingredientInformation = ["beef", "chicken", "pork", "seafood", "rice", "noodle", "cheese", "potato", "tomato", "mushroom"]
    const value = Info[0];
    const info = Info[1];

    if (value === 'age' || value === 'carbohydrate' || value === 'protein' || value === 'fat') {
      setForm({
        ...form,
        [value] : Number(info)
      })
    } 
}

  return (
    <>
      <Container>
        <ImgContainer>
          <img src={logo} alt="logo" />
        </ImgContainer>
        <Title ff="Playfair Display" fs="2rem" fw="300">FOR:EAT</Title>
        <Title fs="1.5rem" fw="200" mt="1rem" mb="3rem">PERSONALIZE YOUR EXPERIENCE</Title>
        { step === 1 ? <InformationSurvey form={form} propFunction={getInformation} nextSteps={nextSteps} /> : null}
      </Container>
    </>
  )
```

- 상위 컴포넌트에서 getInformation 함수를 정의한다.

- 해당 컴포넌트에서 하위 컴포넌트 InformationSurvey를 import하고, 하위 컴포넌트에서 getInformation 함수를 사용할 함수 이름을 정의해준다. 

  > 하위 컴포넌트에서는 propFunction 이라는 이름의 함수로 getInformation 함수를 사용

</br>

```javascript
import React, { useState } from 'react';


const InformationSurvey = ({form, propFunction, nextSteps}) => {
  const{ gender } = form  // 필요한 키들만 비구조할당으로 선언
  const [womanShow, setWomanShow] = useState(gender);
  const [manShow, setManShow] = useState((gender === null ? false : !gender));

  const survey = (info) => {
    if (info === true) {
      setWomanShow(true);
      setManShow(false);
      propFunction(['gender', true])
    } else {
      setManShow(true)
      setWomanShow(false)
      propFunction(['gender', false])
    }
  }
```

- 하위 컴포넌트에서는 propFunction을 받아서 사용할 수 있다. 
- 전달할 매개변수가 있다면 상위 컴포넌트의 함수와 하위 컴포넌트 함수 모두 작성해야 한다.
