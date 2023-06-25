<template>
  <MainHeder />
  <mainCalculator />

</template>

<script>
import MainHeder from "./components/MainHeder.vue";
import mainCalculator from "./components/mainCalculator.vue";
export default {
  name: "App",
  components: {
    MainHeder: MainHeder,
    mainCalculator: mainCalculator,
   
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
