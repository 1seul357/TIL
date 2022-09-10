# 스피너 적용하기

### 전체 코드

```javascript
import {React, useState, forwardRef, useImperativeHandle} from "react";
import styled from "styled-components";
import { getRecipeList } from "api/CategoryApi";
import Card from "components/commons/Card";
import "assets/css/Pagination.css";
import Pagination from "react-js-pagination";
import { CircularProgress } from "@mui/material";


const Servings = forwardRef((props, ref) => {
  useImperativeHandle(ref, () => ({
    getServingsRecipe(){
      getOneRecipe();
    }
  }))

  const [oneRecipeShow, setOneRecipeShow] = useState(true);
  const [RecipeList, setRecipeList] = useState([]);
  const [totalCount, setTotalCount] = useState(0);
  const [isLoading, setIsLoading] = useState(true);
  const [page, setPage] = useState(1); 

  const handlePageChange = (page) => { 
    window.scrollTo(0, 0)
    setPage(page); 
    if (oneRecipeShow === true) {
      getOneRecipe(page);
    }
  };

  const getOneRecipe = async(page) => {
    setIsLoading(true);
    setOneRecipeShow(true);
    setTwoRecipeShow(false);
    setFourRecipeShow(false);
    setPartyRecipeShow(false);
    if (isNaN(page) === true) {
      setPage(1); 
      page = 1;
    }
    const Recipe = await getRecipeList(page, "One");
    if (Recipe) {
      setRecipeList(Recipe.data);
      setIsLoading(false);
      setTotalCount(Recipe.total_count);
    }
  }

  

  return (
    <Container>
      <div>
        {oneRecipeShow ? <ServingsButton onClick={()=>getOneRecipe(1)} style={{backgroundColor: "#ED8141", color: "white"}}>ONE</ServingsButton> : <ServingsButton onClick={getOneRecipe}>ONE</ServingsButton>}
      </div> 
      {isLoading ? <div style={{display: "flex", justifyContent: "center", marginTop: "2rem"}}><CircularProgress /></div> :
        <CardContainer>
          {RecipeList.map((Recipe, index) => (
            <Card
              key={Recipe.recipe_seq}
              recipeSeq={Recipe.recipe_seq}
              index={index}
              recipeImg={Recipe.images}
              recipeName={Recipe.name}
              recipeKeywords={(Recipe.keywords.length > 1 ? [Recipe.keywords[0].keyword_name, Recipe.keywords[1].keyword_name] : Recipe.keywords[0].keyword_name)}
              recipeCalorie={Recipe.calories}
              recipeRating={Recipe.average_rating}
              likedCount={Recipe.liked_count}
            />
          ))}
        </CardContainer>
      }
      {isLoading ? null :       
      (RecipeList.length !== 0 ?      
        <PageContainer>
          <Pagination 
            activePage={page} 
            itemsCountPerPage={24} 
            totalItemsCount={totalCount} 
            pageRangeDisplayed={5} 
            prevPageText={"‹"} 
            nextPageText={"›"} 
            onChange={handlePageChange}
          />
        </PageContainer> : null
      )}
    </Container>
  );
});

export default Servings;
```

</br>
</br>

### 스피너 적용 단계

```javascript
const [isLoading, setIsLoading] = useState(true);
```

- 페이지가 렌더링되자마자 스피너가 보여야 하므로 useState를 정의하면서 true로 초기값을 설정한다.

```javascript
const Recipe = await getRecipeList(page, "One");
    if (Recipe) {
      setRecipeList(Recipe.data);
      setIsLoading(false);
      setTotalCount(Recipe.total_count);
    }
```

- getRecipeList 함수를 호출하고 값을 리턴받으면 setIsLoading을 false로 바꿔서 스피너가 멈출 수 있도록 만든다.

```javascript
{isLoading ? <div style={{display: "flex", justifyContent: "center", marginTop: "2rem"}}><CircularProgress /></div> :
        <CardContainer>
          {RecipeList.map((Recipe, index) => (
            <Card
              key={Recipe.recipe_seq}
              recipeSeq={Recipe.recipe_seq}
              index={index}
              recipeImg={Recipe.images}
              recipeName={Recipe.name}
              recipeKeywords={(Recipe.keywords.length > 1 ? [Recipe.keywords[0].keyword_name, Recipe.keywords[1].keyword_name] : Recipe.keywords[0].keyword_name)}
              recipeCalorie={Recipe.calories}
              recipeRating={Recipe.average_rating}
              likedCount={Recipe.liked_count}
            />
          ))}
        </CardContainer>
      }
```

- isLoading이 true이면 스피너가 돌아가게끔 만들어주고, false이면 스피너를 감추고, return 받은 데이터 값을 보여주면 된다.
- 이렇게 함수 호출 후 리턴 받은 데이터 값이 있으면 setIsLoding을 false로 바꿔주면 되므로 스피너를 쉽게 구현할 수 있다. 하지만 함수 호출이 아닌 이미 있는 데이터들을 바탕으로 스피너를 구현하는 것은 같은 방식으로 할 수 없다. 이런 경우에는 아래 코드처럼 구현해야 한다.



```javascript
import React, {useState, useEffect} from "react";
import styled from "styled-components";
import IngredientSelect from "components/recommend/Ingredient/IngredientSelect"
import { CircularProgress } from "@mui/material";



const Ingredient = () => {
  const [isLoading, setIsLoading] = useState(true);

  useEffect(()=>{
    let timer = setTimeout(()=>{ setIsLoading(false) }, 3500);
    // console.log(timer);
  }, [ isLoading ]);

 

  return (
    <>
      <Container>
          {isLoading ? <CircularProgress style={{display: "flex", justifyContent: "center", marginTop: "2rem"}}/> :
            <IngredientSelect /> 
          }
      </Container>
    </>
  );
};

export default Ingredient;

```

- useState를 통해 isLoading을 true로 만들고, 페이지가 렌더링되자마자 스피너를 띄워준다.

- useEffect를 통해 3.5초가 실행된 후에 isLoading을 false로 만들어서 스피너를 사라지게 하고, <IngredientSelect /> 컴포넌트를 보여준다.

  > useEffect를 통해 시간 설정을 하고, setIsLoading을 바꿔주면 함수 없이도 스피너를 적용할 수 있다.
