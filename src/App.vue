<template>
  <div id="app">
    <div class="headLine">
      <img src="./assets/logo.png">
      <headLabel/>
      <img src="./assets/logo.png">
    </div>
    <div class="iphoneBody">
      <div class="speaker">
      </div>
      <calcFrame/>
      <div class="home">
      </div>
    </div>
  </div>
</template>

<script>
import headLabel from "./components/headLabel";
import calcFrame from "./components/calcFrame";
import calcButton from "./components/calcButton";

export default {
  name: "App",
  components: {
    headLabel,
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

body {
  font-size: 28px;
  font-family: "Lato";
  font-weight: 300;
}

.iphoneBody {
  margin: 0 auto;
  border: 3px solid	#c9ba93;
  border-radius: 75px;
  width: 450px;
  height: 930px;
}

.speaker {
  margin: 56px auto;
  border-radius: 15px;
  width: 80px;
  height: 9px;
  background: black;
  position: relative;
}

.speaker::after{
  content: '';
  width: 20px;
  height: 20px;
  background: black;
  position: absolute;
  left: -50px;
  top: -5px;
  border-radius: 50%;
}
.speaker::before{
  content: '';
  width: 12px;
  height: 12px;
  background: black;
  position: absolute;
  left: 50%;
  transform: translate(-50%);
  top: -45px;
  border-radius: 50%;
}

.home {
  margin: 7px auto;
  width: 78px;
  height: 78px;
  border: 5px solid #c9ba93;
  border-radius: 50%;
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
</style>
