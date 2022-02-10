## 데이터가 없을 시, 레이아웃 깨지는 문제

```vue
<div class="d-flex col-12">                             <!-- col-12 추가 -->
      <div class="col-2">
          <p v-if="img">
            <img :src="img" alt="default-img">
          </p>
          <p v-else>
            <img src="./assets/default.png">
          </p>
          <p>{{ userInfo.nickname }}</p>
          <b-button id="show-btn" @click="showModal" variant="link">개인정보수정</b-button>
      </div>
      <div class="col-5 d-flex justify-content-center">
        	<study-chart :StudyTime="StudyTime"></study-chart>
      </div>
      <div class="col-5">
          <study-point-bar :userInfo="userInfo"></study-point-bar>
          <h5 style="text-align : start;"><strong>관심분야</strong></h5>
          <user-interests :interestList="getInterests()"></user-interests>
      </div>
</div>
```

**문제상황**

관심분야에 데이터가 없거나, 적은 경우 레이아웃이 깨져서 왼쪽으로 쏠리는 현상이 발생했다. 레이아웃을 크게 col-2, col-5, col-5로 설정했는데, 이것과 상관없이 데이터끼리 겹치는 문제가 있었다.



**해결방법**

3개의 div를 감싸고 있는 부모 div에 col-12를 설정하면 위와 같은 문제를 해결할 수 있다.