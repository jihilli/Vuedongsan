<template>
    <img alt="Vue logo" src="./assets/logo.png" />
    <div>
        <!-- 데이터바인딩(데이터 집어넣기) 
          1) 속성 - :속성="데이터이름"
          2) HTML 내 - {{ 데이터이름 }} -->

        <h4 class="red" :style="스타일">{{ products[0] }}</h4>
        <p>{{ price1 }}만원</p>
    </div>
    <div>
        <h4>{{ products[1] }}</h4>
        <p>{{ price2 }}만원</p>
    </div>
    <div>
        <h4>{{ products[2] }}</h4>
        <p>{{ price3 }}만원</p>
    </div>
</template>

<script>
export default {
    name: "App",
    // vue의 데이터 보관함 - object 자료 형식으로 저장
    data() {
        return {
            스타일: "color : blue",
            products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
            price1: 60,
            price2: 70,
            price3: 80,
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
    margin-top: 60px;
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
