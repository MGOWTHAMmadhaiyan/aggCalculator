<template>
  <el-row>
    <AgeCalculator></AgeCalculator>
  </el-row>
</template>

<script>
import AgeCalculator from "./components/AgeCalculator.vue";
export default {
  name: "App",
  components: {
    AgeCalculator,
  },
};
</script>

<style scoped>
</style>
