<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col">
          <home/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Home from "./views/home/Home";
import { ref } from "@vue/composition-api"


export default {
  setup() {
    const isOpen = ref(false);
    return { isOpen };
  },
  name: 'App',
  components: {
     Home
  }
}
</script>

<style>

</style>
