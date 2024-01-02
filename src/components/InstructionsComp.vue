<template>
<div class="instruction-page pageEnter">
    <h2 :style="{'color': 'white', 'font-size': '40px'}">Counting Sheeps</h2>
    <p :style="{'color': 'white' , 'font-size': '30px', 'margin-bottom': '0px'}">{{ instructions.title }}</p>
    <p :style="{'color': 'white', 'font-size': '25px'}">{{ instructions.paragraph }}</p>
    <div class="btn-wrap">
        <button :style="{minHeight: '25px'}" @click="$emit('confirmInstructions', true)" :class="{'none': !display}">Let's Play</button>
    </div>
    <img :class="{'none': !display}" src="../assets/sheeps-intro.gif"/>
</div>
</template>

<script setup>
import {ref} from 'vue'
let display = ref(false)
const instructions = {
    title: `Let's aid your sleep!`,
    paragraph: 'Count sheep by clicking them. As you count, the screen gradually darkens until you drift off. :)'
}
setTimeout(() => {
    display.value = true
}, 2000)

</script>

<style>
.instruction-page {
    display: flex;
    flex-direction: column;
    width: 90%;
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
    }
    p {
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

