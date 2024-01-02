<template>
<div class="instruction-page pageEnter">
    <h2>Counting Sheeps</h2>
    <p>{{ msg }}</p>
    <div class="btn-wrap">
        <button @click="$emit('confirmInstructions', true)" :class="{'none': !display}">Let's Play</button>
    </div>
    <img :class="{'none': !display}" src="../assets/sheeps-intro.gif"/>
</div>
</template>

<script setup>
// import ButtonComp from './ButtonComp.vue';
import {ref} from 'vue'
let display = ref(false)
const msg = 'We will help you to fall a sleep. In this game you will count sheeps by clicking them. every time you count a sheep the screen will become a bit darker until you will fall a sleep :)'
setTimeout(() => {
    display.value = true
}, 2000)

</script>

<style>
.instruction-page {
    display: flex;
    flex-direction: column;
    width: 100%;
    height: 105vh;
    background-color: black;
    padding-left: 20px;
    padding-right: 20px;
    margin-block-end: 0px;
    img {
        width: 100%;
        bottom: 0;
    }
    .btn-wrap {
        display: flex;
        justify-content: center;
        button {
        border-radius: 50%;
        padding: 5px;
        width: 70px;
        height: 70px;
    }
    }
    .visible {
        display: 'block';
    }

    .none {
        display: 'none';
    }
    h2 {
        font-size: 40px;
        color: white;
    }
    p {
        color: white;
        font-size: 30px;
    }
}

.pageEnter {
    animation: pageEnter 2s linear;
}

@keyframes pageEnter {
    0% { height: 0vh;}
    100% { height: 100vh;}
}
</style>

