<template>
  <div id="app" class="flex justify-center items-center h-screen  bg-gradient-to-l from-gray-400 to-gray-700">
    <div class="bg-[#021526] w-100 p-10 border-1 border-[#0000] rounded-2xl shadow-[-3px_1px_55px_0px_rgba(255,_255,_255,_0.05)]">
      <div class="mb-3">
        <button type="button" @click="toggleHistory" class="text-white bg-gray-800 hover:bg-gray-700 focus:outline-none focus:ring-4 focus:ring-gray-300 font-medium rounded-full text-sm px-5 py-2.5 me-2 mb-2 dark:bg-gray-800 dark:hover:bg-gray-700 dark:focus:ring-gray-700 dark:border-gray-700">history</button>
      </div>
      
      <div class="mb-5">
        <input v-model="displayValue" type="text" id="first_name" class="text-end h-15 bg-gray-50 border border-gray-300 text-gray-900 text-xl rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" disabled />
      </div>

      <div class="grid grid-cols-4 gap-2">
        <button class="text-white bg-gray-800 hover:bg-gray-700 focus:outline-none focus:ring-4 focus:ring-gray-900 font-medium rounded-full text-sm px-5 py-2.5 me-0.5 mb-1" v-for="(button, index) in buttons" :key="index" :class="button.class" @click="button.action">
          <span v-if="typeof button.value === 'number'">{{ button.value }}</span>
          <span v-else>
             <i v-if="button.class === 'delete'" class="fa fa-backspace"></i>
             <i v-if="button.class === 'minus'" class="fa-solid fa-minus"></i>
             <i v-if="button.class === 'plus'" class="fa-solid fa-plus"></i>
             <i v-if="button.class === 'divide'" class="fa-solid fa-divide"></i>
             <i v-if="button.class === 'multiply'" class="fa-solid fa-xmark"></i>
             <i v-if="button.class === 'result'" class="fa-solid fa-equals"></i>
             <i v-if="button.class === 'clear'" class="fa-solid fa-c"></i>
            <span v-else>{{ button.value }}</span>
          </span>
        </button>
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

      buttons: [
        { value: 1, action: () => this.appendNumber(1) },
        { value: 2, action: () => this.appendNumber(2) },
        { value: 3, action: () => this.appendNumber(3) },
        { value: '', class: 'delete', action: this.eraseLastCharacter },
        { value: 4, action: () => this.appendNumber(4) },
        { value: 5, action: () => this.appendNumber(5) },
        { value: 6, action: () => this.appendNumber(6) },
        { value: '', class: 'minus', action: () => this.appendOperator('-') },
        { value: 7, action: () => this.appendNumber(7) },
        { value: 8, action: () => this.appendNumber(8) },
        { value: 9, action: () => this.appendNumber(9) },
        { value: '', class: 'plus', action: () => this.appendOperator('+') },
        { value: 0, action: () => this.appendNumber(0) },
        { value: '.', class: '', action: () => this.appendOperator('.') },
        { value: '', class: 'multiply', action: () => this.appendOperator('*') },
        { value: '', class: 'divide', action: () => this.appendOperator('/') },
        { value: '', class: 'clear', action: this.clearDisplay },
        { value: '', class: 'result', action: this.calculateResult }
      ]
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
}



.result {
  width: 185px;
  margin-left: 50px;
}

.clear {
  width: 125px;
}

.minus, .plus, .divide, .multiply {
  background-color: #EFB036;
}



</style>
