<template>
    <!-- <div v-for="(원룸, i) in 원룸들" :key="i">
        <img :src="원룸.image" class="room-img" />
        <h4 @click="selectProduct(i)">{{ 원룸들[i].title }}</h4>
        <p>{{ 원룸.price }}원</p>
        <button @click="increase2[i]">허위매물신고</button> <span>신고수 : {{ 신고수2[i] }}</span>
    </div> -->
    <div>
        <img :src="원룸.image" class="room-img" />
        <!-- custom event 
            $emit('작명', 보낼 데이터) / $emit('함수명')
            - 자식 -> 부모 데이터 바꾸고 싶을 때(부모에게 메세지 보낼 때) 사용! 
            부모가 메세지 수신할 땐 - @작명한 거=""-->
        <h4 @click="$emit('openModal', 원룸.id)">{{ 원룸.title }}</h4>

        <!-- <p @click="send">{{ 원룸.title }}</p> -->

        <p>{{ 원룸.price }}원</p>
        <!-- <button @click="increase2[i]">허위매물신고</button> <span>신고수 : {{ 신고수2[i] }}</span> -->
    </div>
</template>

<script>
export default {
    name: "CardVue",
    props: { 원룸: Object },
    methods: {
        send() {
            // $emit을 함수 안에서 하고 싶으면
            // 주의할 점! props든 data든 $변수든 밑에서 쓸때는 전부 this. 앞에 써주기
            this.$emit("openModal", this.원룸.id);
        },
    },
};
</script>

<style></style>
