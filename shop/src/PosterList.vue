<template>
    <div class="posterBox">
        <img :src="posterData.image" class="posterImg" />
        <p class="posterName" @click="$emit('eventModal', posterData.id)">{{ posterData.title }}</p>
        <p>{{ posterData.price }}원</p>
    </div>
</template>

<script>
export default {
    props: {
        posterData: Object,
    },
};
</script>

<style>

</style>