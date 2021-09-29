<template>
  <div :class="{ loader: true, fadeout: !isLoading }" class="d-flex flex-column" >
      <img class="" src="../assets/bluewave.svg" alt=""/>
       <div class="position-absolute top-50 start-50 translate-middle"> Q&A Game</div>
       <img class="" src="../assets/yellowwave.svg" alt="">
  
  </div>
  
</template>

<script>
export default {
  name: "LoadingScreen",
  props: ["isLoading"]
};
</script>

<style>

.loader {
  background-color: #ca2929;
  bottom: 0;
  color: white;
  display: block;
  font-size: 32px;
  left: 0;
  overflow: hidden;
  position: fixed;
  right: 0;
  text-align: center;
  top: 0;
}

.fadeout {
  animation: fadeout 2s forwards;
}

@keyframes fadeout {
  to {
    opacity: 0;
    visibility: hidden;
  }
}
</style>
