<template>
  <div id="app">
    <div class="calculator">

      <div class="historyBtn">
        <button @click="toggleHistory">history</button>
      </div>
      
      <div class="display">
        <input v-model="displayValue" disabled/>
      </div>

      <div class="buttons">
        <button @click="appendNumber(1)">1</button>
        <button @click="appendNumber(2)">2</button>
        <button @click="appendNumber(3)">3</button>
        <button class="operator" @click="eraseLastCharacter">DEL</button>
        <button @click="appendNumber(4)">4</button>
        <button @click="appendNumber(5)">5</button>
        <button @click="appendNumber(6)">6</button>
        <button class="operator" @click="appendOperator('-')">-</button>
        <button @click="appendNumber(7)">7</button>
        <button @click="appendNumber(8)">8</button>
        <button @click="appendNumber(9)">9</button>
        <button class="operator" @click="appendOperator('+')">+</button>
        <button @click="appendNumber(0)">0</button>
        <button class="operator" @click="appendOperator('.')"><span>.</span></button>
        <button class="operator" @click="appendOperator('*')">*</button>
        <button class="operator" @click="appendOperator('/')">/</button>
        <button class="operator" @click="clearDisplay">RESET</button>
        <button class="operator" @click="calculateResult">=</button>
      </div>
    </div>
    <div class="history" v-if="showHistory">
      <h6>recent answers:</h6>
        <ul>
          <li v-for="(item, index) in history" :key="index"> {{ item }}</li>
        </ul>
      </div>
  </div>

</template>

<script>
export default {
  data() {
    return {
      displayValue: "",
      history: [],  
      showHistory: false,
    };
  },

  methods: {
    appendNumber(number) {
      this.displayValue += number;
    },

    clearDisplay() {
      this.displayValue = "";
    },

    appendOperator(operator) {
      if (this.displayValue && !/[+\-/*]$/.test(this.displayValue)) {
        this.displayValue += operator;
      }
    },

    eraseLastCharacter() {
      this.displayValue = this.displayValue.slice(0, -1);
    },

    toggleHistory() {
      this.showHistory = !this.showHistory;
    },

    
    calculateResult() {
      try {
        const result = eval(this.displayValue);
        this.displayValue = result.toString();

        if (!isNaN(result) && result > 9999) {
          this.displayValue = result.toLocaleString();
        }

        this.history.push(`${this.displayValue}`);

        if (this.history.length > 5) {
          this.history.shift();
        }
      } catch (e) {
        this.displayValue = "error";
      }
    },
  },
};
</script>


<style scoped>
#app {
  font-family: "Crimson Text", serif;
  text-align: center;
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: #4C585B;
  
}

.calculator {
  display: inline-block;
  border: 2px solid #4C585B;
  padding: 30px;
  border-radius: 10px;
  margin-right:20px;
  background-color: #4C585B;
  -webkit-box-shadow: -5px 0px 42px 0px rgba(156,156,156,1);
  -moz-box-shadow: -5px 0px 42px 0px rgba(156,156,156,1);
  box-shadow: -5px 0px 42px 0px rgba(156,156,156,1);
}

.display input {
  width: 400px;
  height: 70px;
  font-weight: bolder;
  font-size: 2em;
  text-align: right;
  margin-bottom: 20px;
  padding-right: 10px;
  border-radius: 4px;
  border: 1px solid #4C585B;
  background-color: #f7f7f7;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 10px;
  background: #f7f7f7;
  padding: 15px 15px;
  border-radius: 5px;
  background-color: #7E99A3;
}

button {
  font-size: 1.1em;
  padding: 10px;
  cursor: pointer;
  border-radius: 5px;
  color: black;
  background-color: #f7f7f7;
  transition: 0.1s ease-in-out;
}


button:hover {
  background-color: #4C585B;
  color: #fff;
}

.operator {
  background-color: #A5BFCC;
  color: black;
}
.history {
  text-align: start;
  padding: 40px;
  min-width: 200px;
  height: 60%;
}

.history h6 {
  font-size: 20px;
  font-weight: bold;
  color: #fff;
}

.history li {
  font-size: 25px;
  color: #fff;
}

.historyBtn {
  text-align: start;
  margin-bottom: 20px;
}

.historyBtn button {
  background-color: #A5BFCC;
  border: none;
  padding: 8px 16px;
  color: #000;
  font-size: 15px;
  text-transform: lowercase;
  letter-spacing: 1px;
}

.historyBtn button:hover {
  background-color: #7E99A3;
  color: #000;
}

</style>
