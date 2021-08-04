<template>
  <div class="main__section">
    <Calender />
  </div>
</template>

<script>
import Calender from "./components/Calender.vue";
export default {
  components: { Calender },
};
</script>

<style>
.main__section {
  width: 100%;
  height: 100vh;
}
</style>
