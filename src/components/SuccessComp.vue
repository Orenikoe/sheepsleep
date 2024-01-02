<template>
    <div class="gif-wrap">
        <h3 :style="{'color': 'white'}">Good Night!</h3>
        <img class="successgif" src="../assets/good-night.png"/>
    </div>
    </template>
    
    <script setup>
    

    </script>
    
    <style>
    .gif-wrap {
        background-color: black;
        width: 100%;
        height: 100vh;
        display: flex;
        justify-content: center;
        overflow: hidden;
        h3 {
            color: white;
            -webkit-text-fill-color: white;
        }
    }

    .successgif {
        position: absolute;
        top: 20%;
        animation: moonRise 2s ease-in;
    }

    @keyframes moonRise {
        0% {top: 100%;}
        100% {top: 20%;}
        
    }

    </style>
    
    