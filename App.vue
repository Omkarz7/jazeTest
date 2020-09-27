<template>
    <router></router>
</template>

<script>
import router from "./router/router.vue";
export default {
  components:{
    router
  }
}
</script>

<style>
.container {
  background-color: white;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.text-color-primary {
  color: blue;
}
</style>
