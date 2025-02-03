<template>
  <div id="app" class="flex justify-center items-center h-screen  bg-gradient-to-l from-gray-400 to-gray-700">
    <div class="bg-[#021526] w-100 p-7 border-1 border-[#0000] rounded-2xl shadow-[-3px_1px_55px_0px_rgba(255,_255,_255,_0.05)]">
      
      
      <div class="flex">
          <div class="basis-64 mb-4">
            <button type="button" 
                  @click="toggleHistory" 
                  class="text-white bg-gray-800 hover:bg-gray-700 focus:outline-none focus:ring-4 focus:ring-gray-300 font-medium rounded-full text-sm px-5 py-2.5 me-2 mb-2 dark:bg-gray-800 dark:hover:bg-gray-700 dark:focus:ring-gray-700 dark:border-gray-700">
                  <i class="fa-solid fa-clock-rotate-left"></i>
            </button>
        </div>

        <div class="basis-64 mb-4 text-end">
            <button type="button" 
                  @click="toggleCurrencyConverter" 
                  class="text-white bg-gray-800 hover:bg-gray-700 focus:outline-none focus:ring-4 focus:ring-gray-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2 dark:bg-gray-800 dark:hover:bg-gray-700 dark:focus:ring-gray-700 dark:border-gray-700">
                  currency
            </button>
        </div>
      </div>
      
      <!--History Modal-->
      <div v-if="showHistory" class="fixed inset-0 flex items-center justify-center bg-transparent">
        <div class="bg-white bg-opacity-80 backdrop:blur-md p-4 rounded-lg shadow-lg w-100 h-50 mt-80">
          <div class="flex justify-between items-center">
            <h2 class="text-lg font-semibold">History</h2>
            <button @click="toggleHistory" class="text-gray-500  hover:text-gray-700">✖</button>
          </div>
          <div class="mt-3">
            <ul v-if="history.length">
              <li v-for="(item, index) in history" :key="index" class="text-gray-700 mb-1">
                {{ item }}
              </li>
            </ul>
            <p v-else class="text-gray-400">No history available</p>
          </div>
        </div>
      </div>

      <!--Currency Converter Modal-->
      <div v-if="showCurrencyConverter" class="fixed inset-0 flex items-center justify-center bg-transparent">
       <div class="bg-white bg-opacity-80 backdrop-blur-md p-4 rounded-2xl shadow-lg w-100 h-126.5">
        <div class="flex justify-between items-center">
          <h2 class="text-lg font-semibold">Currency Converter</h2>
          <button @click="toggleCurrencyConverter" class="text-gray-500 hover:text-gray-700">✖</button>
        </div>
    
        <div class="mt-30">

          <p v-if="convertedAmount !== null" class="mb-3 text-gray-700 text-center">
            Converted Amount: <strong>{{ convertedAmount }}</strong> {{ toCurrency }}
          </p>
          
          <input 
            v-model="amount" 
            type="number" 
            placeholder="Enter amount" 
            class="w-full p-2 border rounded-lg text-gray-700">

          <div class="flex flex-col justify-between mt-3">
            <select v-model="fromCurrency" class="p-2 border rounded-lg w-ful mb-3">
              <option v-for="(rate, currency) in exchangeRates" :key="currency" :value="currency">
                {{ currency }}
              </option>
            </select>

            <span class="text-center mb-2 mt-2"><i class="fa-solid fa-arrow-down-long"></i></span>

             <select v-model="toCurrency" class="p-2 border rounded-lg full">
                <option v-for="(rate, currency) in exchangeRates" :key="currency" :value="currency">
                  {{ currency }}
                 </option>
              </select>
          </div>

            <button 
              @click="convertCurrency" 
              class="w-full mt-3 bg-gray-600 text-white p-2 rounded-lg hover:bg-gray-800">
              Convert
            </button>
       </div>
     </div>
    </div>

      




      <div class="mb-5">
        <input v-model="displayValue"
               type="text" 
               id="first_name" 
               class="text-end h-15 bg-gray-50 border border-gray-300 text-gray-900 text-xl rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" disabled />
      </div>

      <div class="grid grid-cols-4 gap-2">
        <button 
          class="text-white bg-gray-800 hover:bg-gray-700 focus:outline-none focus:ring-4 focus:ring-gray-900 font-medium rounded-full    text-sm px-5 py-2.5 me-0.5 mb-1" 
          v-for="(button, index) in buttons" 
          :key="index" :class="button.class" 
          @click="button.action">
          <span v-if="typeof button.value === 'number'">{{ button.value }}</span>
          <span v-else>
             <i v-if="button.class === 'delete'" class="fa fa-backspace"></i>
             <i v-if="button.class === 'minus'" class="fa-solid fa-minus"></i>
             <i v-if="button.class === 'plus'" class="fa-solid fa-plus"></i>
             <i v-if="button.class === 'divide'" class="fa-solid fa-divide"></i>
             <i v-if="button.class === 'multiply'" class="fa-solid fa-xmark"></i>
             <i v-if="button.class === 'result'" class="fa-solid fa-equals"></i>
             <i v-if="button.class === 'squareRoot'" class="fa-solid fa-square-root-variable"></i>
            <span v-else>{{ button.value }}</span>
          </span>
        </button>
      </div>
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
      showCurrencyConverter: false,
      amount: null,
      toCurrency: "EUR",
      convertedAmount: null,
      exchangeRates: {
        USD: 1,   
        EUR: 0.85,
        GBP: 0.75,
        JPY: 110.53,
        PHP: 56.25 
      },
      buttons: [
        { value: '%', class: 'percent', action: this.percent },
        { value: 'x²', class: 'xSquared', action: this.xSquared },
        { value: 'CE', class: 'clear', action: this.clearDisplay },
        { class: 'delete', action: this.eraseLastCharacter },
        { class: 'squareRoot', action: this.squareRoot },
        { value: 'Oz', class: 'ounce', action: this.poundsToOz},
        { value: 'kg', class: 'kilogram', action: this.poundsToKg},
        { class: 'divide', action: () => this.appendOperator('/') },
        { value: 7, action: () => this.appendNumber(7) },
        { value: 8, action: () => this.appendNumber(8) },
        { value: 9, action: () => this.appendNumber(9) },
        { class: 'multiply', action: () => this.appendOperator('*') },
        { value: 4, action: () => this.appendNumber(4) },
        { value: 5, action: () => this.appendNumber(5) },
        { value: 6, action: () => this.appendNumber(6) },
        { class: 'minus', action: () => this.appendOperator('-') },
        { value: 1, action: () => this.appendNumber(1) },
        { value: 2, action: () => this.appendNumber(2) },
        { value: 3, action: () => this.appendNumber(3) },
        { class: 'plus', action: () => this.appendOperator('+') },
        { value: '.', class: '', action: () => this.appendOperator('.') },
        { value: 0, action: () => this.appendNumber(0) },
        { class: 'result', action: this.calculateResult }
      ]
    };
  },

  methods: {

    toggleCurrencyConverter() {
    this.showCurrencyConverter = !this.showCurrencyConverter;
    },

    convertCurrency() {
      if (this.amount && this.fromCurrency && this.toCurrency) {
        let rate = this.exchangeRates[this.toCurrency] / this.exchangeRates[this.fromCurrency];
        this.convertedAmount = (this.amount * rate).toFixed(2);
      }
    },

    toggleHistory() {
      this.showHistory = !this.showHistory;
    },

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

    squareRoot() {
      this.displayValue = Math.sqrt(this.displayValue);
    },

    percent() {
      this.displayValue = this.displayValue / 100;
    },

    poundsToKg() {
      this.displayValue = this.displayValue / 1000;
    },

    poundsToOz() {
      this.displayValue = this.displayValue * 16;
    },

    xSquared() {
      this.displayValue = Math.pow(this.displayValue, 2);
    },

    calculateResult() {
      try {
        const operation = this.displayValue;
        const result = eval(this.displayValue);
        this.displayValue = result.toString();

        if (!isNaN(result) && result > 999) {
          this.displayValue = result.toLocaleString();
        } else {
          this.displayValue = result.toString();
        }

        this.history.push(`${operation} = ${this.displayValue}`);

        if (this.history.length > 5) {
          this.history.shift();
        }
      
      } catch (e) {
        this.displayValue = "";
      }
    },
  },
};
</script>


<style scoped>

#app {
  font-family: "Crimson Text", serif;  
}

.minus, .plus, .divide, .multiply {
  background-color: #EFB036;
}

.result {
  width: 165px;
  margin-left: 0px;
}

</style>
