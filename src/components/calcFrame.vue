<template>
  <div class="calc">
    <div class="screen"> {{currentState || '0'}}</div>
    <calcButton @click.native="clear" class="specialChar1" v-bind:button="'AC'"/>
    <calcButton class="specialChar1" v-bind:button="'+/-'"/>
    <calcButton class="specialChar1" v-bind:button="'%'"/>
    <calcButton class="specialChar2" v-bind:button="'÷'"/>
    <calcButton @click.native="addSymbol('7')" v-bind:button="'7'"/>
    <calcButton @click.native="addSymbol('8')" v-bind:button="'8'"/>
    <calcButton @click.native="addSymbol('9')" v-bind:button="'9'"/>
    <calcButton class="specialChar2" v-bind:button="'×'"/>
    <calcButton @click.native="addSymbol('4')" v-bind:button="'4'"/>
    <calcButton @click.native="addSymbol('5')" v-bind:button="'5'"/>
    <calcButton @click.native="addSymbol('6')" v-bind:button="'6'"/>
    <calcButton class="specialChar2" v-bind:button="'-'"/>
    <calcButton @click.native="addSymbol('1')" v-bind:button="'1'"/>
    <calcButton @click.native="addSymbol('2')" v-bind:button="'2'"/>
    <calcButton @click.native="addSymbol('3')" v-bind:button="'3'"/>
    <calcButton class="specialChar2" v-bind:button="'+'"/>
    <calcButton class="longButton" v-bind:button="'0'"/>
    <calcButton @click.native="addDot" v-bind:button="'.'"/>
    <calcButton class="specialChar2" v-bind:button="'='"/>

  </div>
</template>

<script>
import calcButton from "./calcButton";

export default {
  name: "calcFrame",
  components: {
    calcButton
  },
  data() {
    return {
      currentState: "",
      currentOperator: null,
      oldState: null
    };
  },
  methods: {
    addSymbol: function(symbol) {
      this.currentState += symbol;
    },
    clear: function() {
      this.currentState = "";
    },
    addDot: function() {
      this.currentState.indexOf(".") === -1 ? this.addSymbol(".") : this.currentState;
    }
  },
  computed: {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  font-size: 1.2em;
}
.calc {
  border-radius: 5%;
  overflow: hidden;
  background: black;
  display: grid;
  color: white;
  width: 400px;
  margin: 0 auto;
  grid-template-columns: repeat(4, 100px [col-start]);
  grid-template-rows: repeat(7, 100px [row-start]);
}

.screen {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  padding: 0 15px;
  font-size: 3.5em;
  color: white;
  grid-column-start: 1;
  grid-column-end: 5;
  grid-row-start: 1;
  grid-row-end: 3;
  text-align: right;
}

.longButton {
  grid-column-start: 1;
  grid-column-end: 3;
  border-top-left-radius: 25% 50%;
  border-bottom-left-radius: 25% 50%;

  border-top-right-radius: 25% 50%;
  border-bottom-right-radius: 25% 50%;
}

.specialChar1 {
  color: black;
  background: #d6d6d6;
}

.specialChar2 {
  font-size: 1.4em;
  background: orange;
}
</style>
