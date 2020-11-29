<template>
  <div id="app">
    <Store />
  </div>
</template>

<script>
import Store from "./views/Store";
export default {
  components: {
    Store
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  outline: 0;
  box-sizing: border-box;
}

body {
  font-family: "Roboto", sans-serif;
}

#app {
  display: flex;
  flex-direction: column;
  height: 100vh;
  text-align: center;
}
</style>
