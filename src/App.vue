<template>
  <div id="app">
    <div class="headLine">
      <img src="./assets/logo.png">
      <HelloWorld/>
      <img src="./assets/logo.png">
    </div>
    <calcFrame/>

  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld";
import calcFrame from "./components/calcFrame";
import calcButton from "./components/calcButton";

export default {
  name: "App",
  components: {
    HelloWorld,
    calcFrame,
    calcButton
  }
};
</script>

<style>
img {
  width: 50px;
  height: 50px;
}

.headLine {
  display: flex;
  align-items: center;
  justify-content: center;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
}
body {
  font-size: 28px;
  font-family: "Lato";
  font-weight: 300;
}
</style>
