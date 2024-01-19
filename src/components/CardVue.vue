<template>
    <!-- <div v-for="(원룸, i) in 원룸들" :key="i">
        <img :src="원룸.image" class="room-img" />
        <h4 @click="selectProduct(i)">{{ 원룸들[i].title }}</h4>
        <p>{{ 원룸.price }}원</p>
        <button @click="increase2[i]">허위매물신고</button> <span>신고수 : {{ 신고수2[i] }}</span>
    </div> -->
    <div>
        <img :src="원룸.image" class="room-img" />
        <h4>{{ 원룸.title }}</h4>
        <p>{{ 원룸.price }}원</p>
        <button @click="increase2[i]">허위매물신고</button> <span>신고수 : {{ 신고수2[i] }}</span>
    </div>
</template>

<script>
export default {
    name: "CardVue",
    props: { 원룸: Object },
    methods: {},
};
</script>

<style></style>
