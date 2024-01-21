<template>
    <div class="black-bg" v-if="모달창열렸니 == true">
        <div class="white-bg">
            <img :src="원룸들[누른거].image" style="width: 100%" />
            <h4>{{ 원룸들[누른거].title }}</h4>
            <p>{{ 원룸들[누른거].content }}</p>
            <!-- 유저가 <input>에 입력한 값을 데이터로 저장하는 방법 1) 
            <input @input="month = $event.target.value" /> -->
            <!-- 방법 2) v-model('데이터이름') : '여기에 입력한 데이터를 밑에 저장해줘' -->
            <input v-model.number="month" />
            <!-- 사용자가 <input>에 입력한 것은 (초기값을 숫자로 해줘도) 전부 문자자료형!
                -> v-model.number 로 숫자형으로 설정해주기 -->
            <p>{{ month }}개월 선택함 : {{ 원룸들[누른거].price * month }}원</p>

            <!-- ** props로 받아온 데이터는 read-only이므로, 받아온 거 수정하면 큰일 남! -->
            <!-- <button @click="모달창열렸니 = false">X</button> -->
            <button @click="$emit('closeModal', false)">X</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "ModalVue",
    data() {
        return {
            month: 1,
        };
    },
    // watcher - 데이터 감시하기 ex)사용자가 문자로 입력하는지 감시하는 등
    // 감시할 데이터 함수형으로 작성해주기 -> watch : { 감시할데이터(){} }
    watch: {
        // month라는 데이터가 변할 때마다 여기있는 코드 실행
        month(a) {
            // parameter는 최대 2개까지 입력 가능
            // -> ex. month(a, b) - a : 변경 될 month 데이터 / b : 변경 전 month 데이터
            if (isNaN(a)) {
                alert("숫자만 입력해주세요");
                this.month = 1;
            }
        },
    },
    // props로 받아온 거 등록하기 - props : {데이터이름 : 자료형이름}
    props: { 원룸들: Array, 누른거: Number, 모달창열렸니: Boolean },
};
</script>

<style>
.black-bg {
    width: 60%;
    height: 50%;
    background: rgba(0, 0, 0, 0.5);
    position: fixed;
    padding: 20px;
    border-radius: 8px;
}

.white-bg {
    width: 100%;
    background: white;
    border-radius: 8px;
    padding: 20px;
}
</style>

<!-- props : 부모도 쓰는 데이터라면, 데이터를 자식컴포넌트에 만들지 않고 부모 컴포넌트에 만들기
(데이터를 위->아래로 전송하는 건 props 사용하면 쉬운데, 역방향은 어렵기 때문) -->

<!-- @input - 입력할 때마다 뭔가를 실행하게 함
     @change - 입력하고 커서 다른 곳 찍으면 뭔가를 실행하게 함 

    <textarea v-model="description"></textarea>
    <select v-model="month">
        <option>1</option>
        <option>2</option>
    </select>
    <input type="checkbox" />
    <input type="range" min="1" max="12" />  -->
