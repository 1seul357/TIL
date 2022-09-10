# 무한 스크롤 사용하기

```javascript
import React, { useState, useEffect } from "react";
import Title from "components/commons/Title";
import { getRecommendRecipeList } from "api/RecommendApi";
import Card from "components/commons/Card";


const FeedRecipeList = () => { 
  const [forYouRecipe, setForYouRecipe] = useState();
  const [youLikeRecipe, setYouLikeRecipe] = useState();
  const [recipeList, setRecipeList] = useState([]);
  const [memberType, setMemberType] = useState();
  const [number, setNumber] = useState(2);


  const getRecipeList = async (type, page) => {
    if (type === "foryou") {
      if (page === 1) {
        setNumber(2);
        setRecipeList([]);
      }
      setForYouRecipe(true);
      setYouLikeRecipe(false);
      const response = await getRecommendRecipeList(type, page);
      setRecipeList(recipeList => [...recipeList, response.data])
      setMemberType(response.member_type)
    } else {
      if (page === 1) {
        setNumber(2);
        setRecipeList([]);
      }
      setForYouRecipe(false);
      setYouLikeRecipe(true);
      const response = await getRecommendRecipeList(type, page);
      setRecipeList(recipeList => [...recipeList, response.data])
      setMemberType(response.member_type)
    }
  }

  
  useEffect(() => {  
    getRecipeList("foryou", 1);
  }, [])

    
  const handleScroll = () => {
    const scrollHeight = document.documentElement.scrollHeight;       // 스크롤 시키지 않았을 때의 전체 높이
    const scrollTop = document.documentElement.scrollTop;             // 스크롤되어 올라간 만큼의 높이
    const clientHeight = document.documentElement.clientHeight;       // 눈에 보이는 만큼의 높이
    if(scrollTop + clientHeight >= scrollHeight) {
      setNumber( number + 1 );
      if (forYouRecipe === true && number <= 4 ) {
        getRecipeList("foryou", number);
      }
      else if (youLikeRecipe === true && number <= 4) {
        getRecipeList("likeyou", number);
      }
    }
  }

  useEffect(() => {
    window.addEventListener('scroll', handleScroll);
      return () => {window.removeEventListener('scroll', handleScroll)}
  })

  
return (
    <>
      <div style={{display: "flex", justifyContent: "center", marginTop: "1rem"}}>
        <div>
          <CategoryButton fs="1.3rem" fw="300" mr="1rem" onClick={()=>getRecipeList("foryou", 1)}>FOR:YOU</CategoryButton>
          {forYouRecipe ? <BorderLine /> : null}
        </div>
        <div>
          <CategoryButton fs="1.3rem" fw="300" ml="1rem" onClick={()=>getRecipeList("likeyou", 1)}>YOU:LIKE</CategoryButton>
          {youLikeRecipe ? <BorderLine ml="1.1rem" /> : null}
        </div>
      </div>
      <CardContainer>
        {recipeList.map((recipe, idx) => 
          ( recipe.map((recipeItem, index) => ( 
            <Card
              key={recipeItem.recipe_seq}
              recipeSeq={recipeItem.recipe_seq}
              index={index}
              recipeImg={recipeItem.images}
              recipeName={recipeItem.name}
              recipeKeywords={(recipeItem.keywords.length > 1 ? [recipeItem.keywords[0].keyword_name, recipeItem.keywords[1].keyword_name] : recipeItem.keywords[0].keyword_name)}
              recipeCalorie={recipeItem.calories}
              recipeRating={recipeItem.average_rating}
              likedCount={recipeItem.liked_count}
            />
          ))) 
        )}
      </CardContainer>
    </>
  )
}

export default FeedRecipeList;
```

- **`Element.scrollHeight`** : 요소 콘텐츠의 총 높이, 바깥으로 넘쳐서 보이지 않는 부분 포함

- `Element.clientHeight` : 눈에 보이는 만큼의 높이
- `Element.scrollTop` : 스크롤되어 올라간 만큼의 높이
- `window.addEventListener('scroll', handleScroll)` : 스크롤 이벤트

만약 **전체 높이**보다 clientHeight + scrollTop의 높이가 커지면 추가적으로 데이터를 요청하면 된다. offset을 변화시켜서 15개씩 총 60개의 데이터를 가져와야 하므로 page는 4이하일 때만 getRecipeList 함수를 실행한다. 

> 주의할 점 : YOU:LIKE와 FOR:YOU 버튼을 클릭할 때마다 setNumber와 setRecipeList를 초기화시켜야 한다. 초기화하지 않으면 기존의 값에 추가로 append되어서 나오기 때문에 올바르지 않은 데이터를 보여주게 된다. 그러므로 버튼이 클릭될 때마다 page는 1로, setRecipeList는 빈 리스트로 만들어줘야 한다.