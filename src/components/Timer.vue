<template>
    <div id="timer__container">
        <span id="minutes">{{ min }}</span>
        <span>:</span>
        <span id="seconds">{{ sec }}</span>
    </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    min: {
        type: Number,
        required: true
    },
    sec: {
        type: [Number, String],
        required: true
    }
})

</script>

<style scoped>
#timer__container {
    color: red;
    font-size: xx-large;
    text-align: center;
    margin: 20px 0;
}
</style>

