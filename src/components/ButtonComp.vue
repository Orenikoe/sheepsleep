  <template>
    <div class="btn">
      <span class="title">Click To Start</span>
      <img class="btn-img" src="../assets/cloud-btn.png"/>
    </div>
  </template>
  
  <script>
  
  
  export default {
  }
  </script>
  
  <style>


.btn {
  top: 50%;
  position: relative;
  animation: CloudMove 2s linear infinite;
.title {
  position: absolute;
  top: 50%;
  left: 37%;
  color: black;
  z-index: 1;
}
.btn-img {
  width: 50%;
  max-width: 200px;
}
}

@keyframes CloudMove {
  0%, 100% { top: 50%; }
  50% { top: 52%; }
}
  </style>
  
  