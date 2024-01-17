<template>
    <div class="menu">
        <!-- Vue의 HTML 반복문 
          1. <태그 v-for="작명 in 반복횟수" :key="작명"> 
          2. <태그 v-for="작명 in 데이터명" :key="작명"> 
           -> 1) 자료 안의 데이터 갯수만큼 반복
              2) 작성한 변수(ex.작명)는 데이터(ex.메뉴들)안의 자료가 됨
          3. <태그 v-for="(작명,i) in 데이터명" :key="i">
          -> 변수 작명 2개까지 가능 : (array내 데이터, 1씩 증가하는 정수)  -->
        <a v-for="(작명, i) in 메뉴들" :key="i">{{ 작명 }}</a>
    </div>

    <!-- 모달창 만들기 -->
    <div class="black-bg" v-if="모달창열렸니 == true">
        <div class="white-bg">
            <h4>상세페이지</h4>
            <p>상세페이지 내용</p>
            <button @click="모달창열렸니 = false">X</button>
        </div>
    </div>

    <!-- 데이터바인딩(데이터 집어넣기) 
          1) 속성 - :속성="데이터이름"
          2) HTML 내 - {{ 데이터이름 }} -->
    <div v-for="(product, i) in products" :key="i">
        <img src="./assets/images/room0.jpg" class="room-img" />
        <h4 :style="스타일" @click="모달창열렸니 = true">{{ product }}</h4>
        <p>{{ prices[i] }}만원</p>
        <!-- 이벤트리스너 : (1) v-on:click="" / (2) @click="" 
        -> 작성할 코드가 길어지면, script 내 함수 작성 후, 함수를 집어넣기-->
        <button @click="increase(i)">허위매물신고</button> <span>신고수 : {{ 신고수[i] }}</span>
    </div>
</template>

<script>
export default {
    name: "App",
    // vue의 데이터 보관함 - object 자료 형식으로 저장 (React의 state)
    data() {
        return {
            스타일: "color : blue",
            메뉴들: ["Home", "Shop", "About"],
            // 제품 관련 데이터
            products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
            prices: [60, 70, 80],
            신고수: [0, 0, 0],
            // 모달창 관련 데이터
            모달창열렸니: false,
        };
    },
    // 함수 만드는 공간
    methods: {
        increase(i) {
            // this. : data 안에 있는 데이터를 가져다가 함수를 만들기 위해 반드시 써야 함
            this.신고수[i]++;
        },
    },
    components: {},
};
</script>

<style>
/* 동적인 UI 만드는 법
  0. HTMK CSS로 디자인 먼저 해주기
  1. UI의 현재 상태를 데이터로 저장해두기
  2. 데이터에 따라 UI가 어떻게 보일지 작성 */
body {
    margin: 0;
}

div {
    box-sizing: border-box;
}

.black-bg {
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    position: fixed;
    padding: 20px;
}

/* 모달창 */
.white-bg {
    width: 100%;
    background: white;
    border-radius: 8px;
    padding: 20px;
}

/* 상단 Nav 메뉴  */
.menu {
    background: darkslateblue;
    padding: 15px;
    border-radius: 5px;
}

.menu a {
    color: white;
    padding: 15px;
}

/* 이미지 */
.room-img {
    width: 100%;
    margin-top: 40px;
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
