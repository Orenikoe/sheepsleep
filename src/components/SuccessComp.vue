<template>
    <div class="gif-wrap">
        <h3>Good Night!</h3>
        <img class="successgif" src="../assets/success-gif.gif"/>
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
        }
    }

    .successgif {
        position: absolute;
        top: 20%;
    }

    </style>
    
    