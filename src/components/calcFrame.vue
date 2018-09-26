<template>
  <div class="calc">
    <div class="screen"> {{currentState || '0'}} </div>
    <calcButton @click.native="clear" class="specialChar1" v-bind:button="'AC'"/>
    <calcButton @click.native="positiveNegative" class="specialChar1" v-bind:button="'+/-'"/>
    <calcButton @click.native="currentState /= 100"class="specialChar1" v-bind:button="'%'"/>
    <calcButton @click.native="setOperator('/')" class="specialChar2" v-bind:button="'÷'"/>
    <calcButton @click.native="addSymbol('7')" v-bind:button="'7'"/>
    <calcButton @click.native="addSymbol('8')" v-bind:button="'8'"/>
    <calcButton @click.native="addSymbol('9')" v-bind:button="'9'"/>
    <calcButton @click.native="setOperator('*')" class="specialChar2" v-bind:button="'×'"/>
    <calcButton @click.native="addSymbol('4')" v-bind:button="'4'"/>
    <calcButton @click.native="addSymbol('5')" v-bind:button="'5'"/>
    <calcButton @click.native="addSymbol('6')" v-bind:button="'6'"/>
    <calcButton @click.native="setOperator('-')" class="specialChar2" v-bind:button="'-'"/>
    <calcButton @click.native="addSymbol('1')" v-bind:button="'1'"/>
    <calcButton @click.native="addSymbol('2')" v-bind:button="'2'"/>
    <calcButton @click.native="addSymbol('3')" v-bind:button="'3'"/>
    <calcButton @click.native="setOperator('+')" class="specialChar2" v-bind:button="'+'"/>
    <calcButton @click.native="addSymbol('0')"class="longButton" v-bind:button="'0'"/>
    <calcButton @click.native="addDot" v-bind:button="'.'"/>
    <calcButton @click.native="equal" class="specialChar2" v-bind:button="'='"/>

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
      oldState: null,
      operators: {
        "+": (a, b) => {
          return a + b;
        },
        "-": (a, b) => {
          return a - b;
        },
        "*": (a, b) => {
          return a * b;
        },
        "/": (a, b) => {
          return a / b;
        }
      }
    };
  },
  methods: {
    toNumber: function() {
      this.oldState = parseFloat(this.oldState);
      this.currentState = parseFloat(this.currentState);
    },
    addSymbol: function(symbol) {
      if (symbol == 0) {
        this.currentState ? (this.currentState += symbol) : this.currentState;
      } else {
        this.currentState += symbol;
      }
    },
    clear: function() {
      this.currentState = "";
    },
    addDot: function() {
      this.currentState == "" ? (this.currentState = "0") : this.currentState;
      this.currentState.indexOf(".") === -1
        ? this.addSymbol(".")
        : this.currentState;
    },
    positiveNegative: function() {
      this.currentState.indexOf("-") === -1 && this.currentState !== ""
        ? (this.currentState = "-".concat(this.currentState))
        : (this.currentState = this.currentState.substr(1));
    },
    setOperator: function(operator) {
      if (this.currentState) {
        this.currentOperator = operator;
        this.oldState = this.currentState;
        this.clear();
        console.log(this.currentState);
      }
    },
    equal: function() {
      if (this.currentState && this.oldState) {
        this.toNumber();
        parseFloat(
          this.operators[this.currentOperator](
            this.oldState,
            this.currentState
          ).toFixed(6)
        ).toString().length > 9
          ? (this.currentState = "999999999")
          : (this.currentState = parseFloat(
              this.operators[this.currentOperator](
                this.oldState,
                this.currentState
              ).toFixed(6)
            ).toString());
      }
    }
  },
  computed: {
    resultLength: function() {
      return this.currentState.length;
    }
  },
  watch: {
    currentState: function() {
      this.currentState.length >= 7
        ? (document.querySelector(".screen").style.fontSize = "2.5em")
        : (document.querySelector(".screen").style.fontSize = "3.5em"); // if many chars, change font-size
      this.currentState.length > 9
        ? (this.currentState = this.currentState.substring(0, 9))
        : this.currentState; // keeping length of 9 chars MAX
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  font-size: 1.2em;
}
.calc {
  border: 3px solid black;
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
