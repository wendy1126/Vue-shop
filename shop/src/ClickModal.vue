<template>
    <div class="blackBg" v-if="openModal == true">
        <div class="whiteBg">
            <img :src="posters[clickPoster].image" style="width: 70%; height: 600px;" />
            <h4>{{ posters[clickPoster].title }}</h4>
            <p>{{ posters[clickPoster].content }}</p>
            <!-- <input @input="month=$event.target.value"> -->
            <input v-model="ea">
            <p> {{ ea }}개 선택함 : {{ posters[clickPoster].price * ea }}원</p>
            <button class="buy" @click="buy()">구입</button>
            <button @click="$emit('closeModal')">닫기</button>
        </div>
    </div>
</template>
  
<script>
export default {
    name: 'ClickModal',
    data() {
        return {
            ea: 1,
        }
    },
    methods: {
        buy() {
            alert('구입 완료 되었습니다.')
        },
    },
    watch: {
        ea(a) {
            if (isNaN(a) == true) {
                alert('문자 입력 금지')
                this.ea = 1;
            } else if (a>5) {
                alert('5개 이하만 구입 가능')
                this.ea = 1;
            }
        },
    },

props: {
    posters: Array,
        clickPoster: Number,
            openModal: Boolean,
    },
};
</script>
  
<style>

</style>
  