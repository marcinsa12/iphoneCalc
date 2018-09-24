<template>
  <div class="calcButton">
    {{ button }}
  </div>
</template>

<script>
export default {
  name: "calcButton",
  data() {
    return {};
  },
  props: ["button"]
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 7px;
  border-radius: 50%;
  background-color: #515151;
  transition: 0.2s;
}
div:active {
  background: rgba(226, 226, 226, 0.7);
}
</style>
