<template v-if="rendered">
  <div class="background" :style="{ backgroundPositionX: bgPositionX + 'px' }">
    <div class="overlay" :style="{ backgroundColor: overlayColor }"></div>
    <div :class="{'sheep': start, 'sheepMove': animate, 'visible': animate, 'none': !animate}" v-if="start" @click="handleClick()" :style="{ '--sheep-Y': sheepLocationY }"></div>
    <ButtonComp :class="{'cloudMoveUp': cloudClicked}" v-if="!start && rendered" @click="initGame"></ButtonComp>
  </div>
  <audio autoplay loop>
      <source src="../assets/success-audio.wav" type="audio/mpeg">
  </audio>
</template>

<script>
import ButtonComp from './ButtonComp.vue';

export default {
    data() {
        return {
            count: 0,
            start: false,
            bgPositionX: 0,
            speed: 1,
            maxClicks: 9,
            bgMoveInterval: null,
            sheepLocationY: '300px',
            animate: true,
            cloudClicked: false,
            rendered: false
        };
    },
    mounted() {this.rendered = true},
    computed: {
        overlayColor() {
            const opacity = Math.min(this.count / this.maxClicks, 1);
            return `rgba(0, 0, 0, ${opacity})`;
        }
    },
    emits: ['gameEnd'],
    methods: {
        moveBackground() {
            this.bgMoveInterval = setInterval(() => {
                this.bgPositionX -= this.speed;
            }, 20); 
        },
        handleClick() {
          this.resetAnimation()
            if (this.count === 8) {
                this.handleVictory()
                this.start = !this.start;
                clearInterval(this.bgMoveInterval);
            }
            ++this.count;
            this.sheepLocationY = `${Math.floor(Math.random() * ((window.innerHeight - 150) - 100 + 1)) + 100}px`;
        },
        initGame() {
          this.cloudClicked = true
            setTimeout(() => this.start = !this.start, 1000)
            this.moveBackground();
        },
        handleVictory() {
          this.$emit('gameEnd', true)
        },
        resetAnimation() {
          this.animate = false;
          
          setTimeout(() => {
          this.animate = true;
          },1);

        }
    },
    components: { ButtonComp }
};
</script>

<style>
.overlay {
  z-index: 1;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.1);
  pointer-events: none; 
  transition: opacity 0.5s ease; 
}

.button { 
  z-index: 2;
  position: absolute;
  background-color: white;
}



.background {
  overflow: hidden;
  position: relative;
  width: 100%;
  height: 100vh;
  background-image: url('../assets/bg-image1.jpg');
  background-repeat: repeat-x; 
  animation: slideBackground linear infinite;
}
.sheep {
  position: absolute;
  transform: scaleX(-1);
  width: 100px;
  height: 100px;
  background-image: url('../assets/sheep.png');
  background-size: cover;
}

.sheepMove {
  animation: sheepMove 5s linear infinite, sheepJump 2s linear infinite
}

.none {
  display: none;
}

.visible {
  display: block
}

.cloudMoveUp {
  animation: cloudMoveUp 1s linear;
}

@keyframes sheepJump {
  0%, 100% { top: var(--sheep-Y, 400px); }
  50% { top: calc(var(--sheep-Y, 400px) + 100px); }
}

@keyframes cloudMoveUp {
  0% { top: 50% }
  100% { top: -10% }
}

@keyframes sheepMove {
  0% { left: -100px; }
  100% { left: calc(100%); }
}

@keyframes slideBackground {
  from {
    background-position: 0 0;
  }
  to {
    background-position: -100% 0; 
  }
}

</style>

