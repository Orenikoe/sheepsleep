<template v-show="bgLoaded">
  <div @load="onBgImageLoad" class="background" :style="{ backgroundPositionX: bgPositionX + 'px' }">
    <div class="overlay" :style="{ backgroundColor: overlayColor }"></div>
    <div :class="{'sheep': start, 'sheepMove': animate, 'visible': animate, 'none': !animate}" v-if="start" @click="handleClick()" :style="{ '--sheep-Y': sheepLocationY }"></div>
    <ButtonComp :class="{'cloudMoveUp': cloudClicked}" v-if="!start" @click="initGame"></ButtonComp>
  </div>
  <audio autoplay loop>
      <source src="../assets/success-audio.wav" type="audio/mpeg">
      <!-- Add multiple source elements for cross-browser compatibility -->
    </audio>
</template>

<script>
import ButtonComp from './ButtonComp.vue';
import {ref} from 'vue'


export default {
  setup() {
    const bgLoaded = ref(false);

    const onBgImageLoad = () => {
      bgLoaded.value = true;
    };

    return {
      bgLoaded,
      onBgImageLoad,
    }},
    data() {
        return {
            count: 0,
            start: false,
            bgPositionX: 0,
            speed: 1,
            maxClicks: 4,
            bgMoveInterval: null,
            sheepLocationY: '300px',
            animate: true,
            cloudClicked: false
        };
    },
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
            }, 20); // Adjust interval for smoother movement
        },
        handleClick() {
          this.resetAnimation()
            if (this.count === 3) {
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
          });

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
  background-color: rgba(0, 0, 0, 0.1); /* Initial color with 10% opacity */
  pointer-events: none; /* Allows click events to pass through the overlay */
  transition: opacity 0.5s ease; /* Smooth transition for opacity change */
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
  height: 100vh; /* Adjust the height of the background */
  background-image: url('../assets/bg-image.jpg');
  background-repeat: repeat-x; /* Repeat the background image horizontally */
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
  0% { left: -100px; } /* Start position */
  100% { left: calc(100%); }
}

@keyframes slideBackground {
  from {
    background-position: 0 0;
  }
  to {
    background-position: -100% 0; /* Adjust the distance to cover the background */
  }
}

</style>

