<template>
    <div class="black-bg" v-if="모달창열렸니 == true">
        <div class="white-bg">
            <img :src="원룸들[누른거].image" style="width: 100%" />
            <h4>{{ 원룸들[누른거].title }}</h4>
            <p>{{ 원룸들[누른거].content }}</p>
            <p>{{ 원룸들[누른거].price }}</p>
            <DiscountBanner />
            <!-- ** props로 받아온 데이터는 read-only이므로, 받아온 거 수정하면 큰일 남! -->
            <!-- <button @click="모달창열렸니 = false">X</button> -->
        </div>
    </div>
</template>

<script>
import DiscountBanner from "./DiscountBanner.vue";

export default {
    name: "ModalVue",
    // props로 받아온 거 등록하기 - props : {데이터이름 : 자료형이름}
    props: { 원룸들: Array, 누른거: Number, 모달창열렸니: Boolean },
    components: {
        DiscountBanner: DiscountBanner, // 내맘대로 작명 : import해서 데려온 이름
    },
};
</script>

<style></style>

<!-- props : 부모도 쓰는 데이터라면, 데이터를 자식컴포넌트에 만들지 않고 부모 컴포넌트에 만들기
(데이터를 위->아래로 전송하는 건 props 사용하면 쉬운데, 역방향은 어렵기 때문) -->
