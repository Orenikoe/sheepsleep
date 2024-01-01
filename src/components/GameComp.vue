<template>
  <div class="background" :style="{ backgroundPositionX: bgPositionX + 'px' }">
    <div class="overlay" :style="{ backgroundColor: overlayColor }"></div>
    <div ref="mySheep" :class="{'sheep': !sheepClicked}" v-if="start" @click="handleClick" :style="{ '--sheep-top': sheepJumpTop }"></div>
    <ButtonComp v-if="!start" @click="initGame"></ButtonComp>
    <span>{{ sheepCount }}</span>
    <!-- Your content -->
  </div>
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
            overlayOpacity: 0,
            maxClicks: 10,
            bgMoveInterval: null,
            sheepJumpTop: '300px',
            sheepClicked: false
        };
    },
    computed: {
        sheepCount() {
            return this.count;
        },
        overlayColor() {
            // Calculate the overlay color dynamically based on the number of clicks
            const opacity = Math.min(this.count / this.maxClicks, 1);
            return `rgba(0, 0, 0, ${opacity})`;
        }
    },
    methods: {
        moveBackground() {
            this.bgMoveInterval = setInterval(() => {
                this.bgPositionX -= this.speed;
            }, 20); // Adjust interval for smoother movement
        },
        handleClick() {
            if (this.count === 9) {
              alert('Time to sleep')
                this.start = !this.start;
                clearInterval(this.bgMoveInterval);
            }
            ++this.count;
            this.sheepJumpTop = `${Math.floor(Math.random() * (700 - 100 + 1)) + 100}px`;
            this.overlayOpacity += 0.1; // Increase opacity by 0.1 on each click
            if (this.overlayOpacity >= 1) {
                // When fully darkened after 10 clicks
                this.overlayOpacity = 1;
                // You can add more functionality here
            }
            // You can add more functionality here
        },
        initGame() {
            this.start = !this.start;
            this.moveBackground();
        },
        bringSheepLeft() {
          this.$refs.mySheep.style.class.r
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
    .sheep {
      position: absolute;
      transform: scaleX(-1);
      width: 100px;
      height: 100px;
      background-image: url('../assets/sheep.png');
      background-size: cover;
      animation: sheepMove 5s linear infinite, sheepJump 2s infinite linear;
    }
}

@keyframes sheepJump {
  0%, 100% { top: var(--sheep-top, 400px); }
  50% { top: calc(var(--sheep-top, 400px) + 100px); }
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

