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
    <DiscountBanner />

    <button @click="priceSort">가격순정렬</button>
    <button @click="sortBack">되돌리기</button>

    <!-- <조건식 > 
    <div v-if="조건식">안녕하세요</div>
    <div v-else-if="조건식2">안녕하세요2</div>
    <div v-else>안녕하세요2</div> -->

    <!-- 모달창 : components & props 
    1. 데이터 보내기 - <자식 :데이터이름(작명)="데이터이름">
        * :(콜론)의 역할? 1) HTML 속성에서 데이터 바인딩 2)props 보내주기 (v-bind)
    2. 자식컴포넌트는 props로 받은 걸 data에 등록해주기
** props로 보내준 데이터는 read-only이므로, 자식컴포넌트가 받아온 props 수정하면 큰일 남! -->

    <!-- < 애니메이션 넣기 > 
        1. {클래스명 : ?} - class명을 조건부로 넣음. ?가 true일 때만 클래스 부여 -->
    <!-- <div class="start" :class="{ end: 모달창열렸니 }"> -->
    <!-- 2. 효과 주고 싶은 요소 <transition name="작명">으로 감싸고, style 활용 -->
    <transition name="fade">
        <ModalVue
            @closeModal="모달창열렸니 = $event"
            v-bind:원룸들="원룸들"
            :누른거="누른거"
            :모달창열렸니="모달창열렸니"
        />
    </transition>

    <!-- 데려온 데이터 활용하기 -->
    <!-- @openModal - 자식이 openModal 이름의 메세지 보내면 JS 실행해주라는 뜻
        자식이 보내준 데이터는 $event 변수에 담겨있음 -->
    <CardVue
        @openModal="
            모달창열렸니 = true;
            누른거 = $event;
        "
        :원룸="원룸들[i]"
        v-for="(작명, i) in 원룸들"
        :key="작명"
    />
    <hr />

    <!-- 데이터바인딩(데이터 집어넣기) 
          1) 속성 - :속성="데이터이름"
          2) HTML 내 - {{ 데이터이름 }} -->
    <div v-for="(product, i) in products" :key="i">
        <img :src="getImagePath(i)" class="room-img" />
        <h4 :style="스타일" @click="selectProduct(i)">{{ product }}</h4>
        <p>{{ prices[i] }}만원</p>
        <!-- 이벤트리스너 : (1) v-on:click="" / (2) @click="" 
        -> 작성할 코드가 길어지면, script 내 함수 작성 후, 함수를 집어넣기-->
        <button @click="increase(i)">허위매물신고</button> <span>신고수 : {{ 신고수[i] }}</span>
    </div>

    <!-- <div>
        <img :src="원룸들[0].image" class="room-img" />
        <h4>{{ 원룸들[0].title }}</h4>
        <p>{{ 원룸들[0].price }}원</p>
    </div> -->
</template>

<script>
// import { apple, apple2 } from "./assets/utils/exampleData.js";
import data from "./assets/utils/data";
// import 컴포넌트
import DiscountBanner from "./components/DiscountBanner.vue";
import ModalVue from "./components/ModalVue.vue";
import CardVue from "./components/CardVue.vue";

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
            신고수2: [],
            // 모달창 관련 데이터
            모달창열렸니: false,
            원룸들: data,
            원룸들오리지널: [...data],
            // -> array/object 데이터의 각각 별개의 사본을 만들 때 사용
            누른거: 0,
        };
    },
    // 함수 만드는 공간
    methods: {
        increase(i) {
            // this. : data 안에 있는 데이터를 가져다가 함수를 만들기 위해 반드시 써야 함
            this.신고수[i]++;
        },
        increase2(i) {
            this.신고수2[i]++;
        },
        getImagePath(index) {
            return require(`./assets/images/room${index}.jpg`);
            // require 함수 : 주어진 모듈(ex. 이미지)을 동적으로 가져오는 데 사용
            // <- require 함수 없이 사용하면 엑박 뜸 ,,
        },
        selectProduct(i) {
            this.모달창열렸니 = true;
            this.누른거 = i;
        },
        priceSort() {
            this.원룸들.sort(function (a, b) {
                // sort 함수는 원본이 변형 됨
                return a.price - b.price;
            });
        },
        sortBack() {
            // 등호로 array를 집어넣으면 '왼쪽 오른쪽 값을 공유해달라'는 뜻임
            // 그래서 this.원룸들 = this.원룸들오리지널; 하면 하다가 안됨
            this.원룸들 = [...this.원룸들오리지널];
        },
    },
    // Script에서 import한 컴포넌트 등록하는 공간
    components: {
        DiscountBanner: DiscountBanner, // 내맘대로 작명 : import해서 데려온 이름
        ModalVue: ModalVue,
        CardVue: CardVue,
    },
};
</script>

<style>
/* 동적인 UI 만드는 법
  0. HTML CSS로 디자인 먼저 해주기
  1. UI의 현재 상태를 데이터로 저장해두기
  2. 데이터에 따라 UI가 어떻게 보일지 작성 */
body {
    margin: 0;
}

div {
    box-sizing: border-box;
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

/* Modal 애니메이션 방법 2 */
/* CSS로 애니메이션 주기
    1. 시작 전 class명
    2. 애니메이션 끝난 후 class명
    3. 그리고 원할 때 2번 class명 부착 */
.start {
    opacity: 0;
    transition: all 1s;
}
.end {
    opacity: 1;
}

/* Modal 애니메이션 방법 2 */
/* 입장 애니메이션 */
/* 시작 시 스타일 */
.fade-enter-from {
    opacity: 0;
}
/*  */
.fade-enter-active {
    transition: all 1s;
}
/* 끝날 때 스타일 */
.fade-enter-to {
    opacity: 1;
}
/* 퇴장 애니메이션 */
/* 시작 시 스타일 */
.fade-leave-from {
    transform: translateY(0px);
}
/*  */
.fade-leave-active {
    transition: all 1s;
}
/* 끝날 때 스타일 */
.fade-leave-to {
    transform: translateY(-1000px);
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
