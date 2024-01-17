<template>
    <div class="menu">
        <!-- Vue의 HTML 반복문 
           1. <태그 v-for="작명 in 반복횟수" :key="작명"> 
           2. <태그 v-for="작명 in 데이터명" :key="작명"> 
            -> 1) 자료 안의 데이터 갯수만큼 반복
               2) 작성한 변수(ex.작명)는 데이터(ex.메뉴들)안의 자료가 됨
           3. <태그 v-for="(작명,i) in 데이터명" :key="i">
            -> 변수 작명 2개까지 가능 : (array내 데이터, 1씩 증가하는 정수) 
        -->
        <a v-for="(작명, i) in 메뉴들" :key="i">{{ 작명 }}</a>
    </div>
    <div v-for="(product, i) in products" :key="i">
        <!-- 데이터바인딩(데이터 집어넣기) 
          1) 속성 - :속성="데이터이름"
          2) HTML 내 - {{ 데이터이름 }} -->
        <h4 :style="스타일">{{ product }}</h4>
        <p>{{ prices[i] }}만원</p>
    </div>
</template>

<script>
export default {
    name: "App",
    // vue의 데이터 보관함 - object 자료 형식으로 저장
    data() {
        return {
            스타일: "color : blue",
            메뉴들: ["Home", "Shop", "About"],
            products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
            prices: [60, 70, 80],
        };
    },
    components: {},
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

/* 상단 Nav 메뉴 만들기  */
.menu {
    background: darkslateblue;
    padding: 15px;
    border-radius: 5px;
}

.menu a {
    color: white;
    padding: 15px;
}
</style>

<!-- 

  {{데이터바인딩}} 하는 이유
1. HTML에 하드코딩 해두면 나중에 변경 어려움 
2. Vue의 실시간 자동 렌더링을 쓰기 위해 (*중요)
  -> data를 변경하면 data와 관련된 HTML에도 실시간으로 반영됨
  -> 자주 데이터가 변경되지 않는 값은 할 필요 X (ex.회사명)

  +) HTML 속성도 데이터바인딩 가능  
  -> :속성="데이터이름"

-->
