  <template v-if="isMounted">
    <div class="btn">
      <span class="title">{{ btnText }}</span>
      <img class="btn-img" src="../assets/cloud-btn.png"/>
    </div>
  </template>
  
  <script>
  
  
  export default {
    props: ['btnText'],
    data() {
      return {
        isMounted: false
      }
    },
    mounted() {
      this.isMounted = true
    }
  }
  </script>
  
  
  <style>


.btn {
  top: 50%;
  position: relative;
  animation: CloudMove 2s linear infinite;
}

.btn-img {
  width: 50%;
  max-width: 200px;
}

.title {
  position: absolute;
  top: 50%;
  left: 37%;
  color: black;
  z-index: 1;
}

@keyframes CloudMove {
  0%, 100% { top: 50%; }
  50% { top: 52%; }
}
  </style>
  
  