<template>
  <div :style="{ backgroundColor: themeColor }" class="app-container">
    <!-- Header with navigation icons -->
    <div class="header">
      <button :class="{ active: currentPage === 'calculator' }" @click="switchPage('calculator')">🧮</button>
      <button :class="{ active: currentPage === 'calculationHistory' }"
        @click="switchPage('calculationHistory')">📜</button>
      <button :class="{ active: currentPage === 'appSettings' }" @click="switchPage('appSettings')">⚙️</button>
    </div>

    <!-- Calculator Page -->
    <div v-if="currentPage === 'calculator'" class="calculator">
      <div class="display" :style="{ fontSize: fontSize + 'px' }">{{ display }}</div>
      <div class="button-container">
        <button v-for="button in buttons" :key="button" @click="handleButtonClick(button)" class="button">
          {{ button }}
        </button>
      </div>
    </div>

    <!-- History Page -->
    <div v-if="currentPage === 'calculationHistory'" class="calculation-history">
      <calculation-history :historyList="history" @resetHistory="resetHistory" />
    </div>

    <!-- Settings Page -->
    <div v-if="currentPage === 'appSettings'" class="app-settings">
      <app-settings :fontSize="fontSize" :themeColor="themeColor" @updateFontSize="updateFontSize"
        @updateThemeColor="updateThemeColor" />
    </div>
  </div>
</template>

<script>
import CalculationHistory from './components/CalculationHistory.vue';
import AppSettings from './components/AppSettings.vue';

export default {
  components: {
    CalculationHistory,
    AppSettings
  },
  data() {
    return {
      display: '',
      history: [],
      buttons: [
        '7', '8', '9', '/', '4', '5', '6', '*',
        '1', '2', '3', '-', '0', '.', '=', '+', 'C', 'CE'
      ],
      currentPage: 'calculator',  // Control which page is displayed
      fontSize: 30,
      themeColor: '#f4f4f4', // Default theme color
    };
  },
  methods: {
    handleButtonClick(button) {
      if (button === 'C') {
        this.display = this.display.slice(0, -1);
      } else if (button === 'CE') {
        this.display = '';
      } else if (button === '=') {
        this.calculate();
      } else {
        this.display += button;
      }
    },
    calculate() {
      try {
        let result = eval(this.display); // Perform calculation
        this.history.push({ calculation: this.display, result: result });
        this.display = result.toString();
      } catch (error) {
        this.display = 'Syntax Error'; // More descriptive error handling
      }
    },
    switchPage(page) {
      this.currentPage = page;
    },
    updateFontSize(newSize) {
      this.fontSize = newSize;
    },
    updateThemeColor(newColor) {
      this.themeColor = newColor;
    },
    resetHistory() {
      this.history = [];
    }
  }
};
</script>

<style scoped>
.app-container {
  max-width: 500px;
  margin: 50px auto;
  padding: 20px;
  border-radius: 20px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  text-align: center;
  background-color: #f4f4f4;
  transition: background-color 0.3s ease;
}

.header {
  display: flex;
  justify-content: space-around;
  margin-bottom: 20px;
}

.header button {
  font-size: 24px;
  padding: 10px;
  cursor: pointer;
  background: none;
  border: none;
  transition: color 0.3s ease;
}

.header button.active {
  color: #4CAF50;
}

.calculator {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.display {
  width: 100%;
  margin-bottom: 20px;
  padding: 20px;
  background-color: #333;
  color: white;
  border: none;
  font-size: 30px;
  text-align: right;
  border-radius: 10px;
}

.button-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 15px;
  margin-top: 10px;
}

button {
  padding: 20px;
  font-size: 20px;
  cursor: pointer;
  background-color: #f1f1f1;
  border: none;
  border-radius: 8px;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #e0e0e0;
}

.calculation-history,
.app-settings {
  padding: 20px;
}

button:active {
  background-color: #bbb;
}

button:focus {
  outline: none;
}
</style>
