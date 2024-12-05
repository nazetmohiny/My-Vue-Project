<template>
  <div>
    <h2>Calculation History</h2>
    <ul>
      <li v-for="(item, index) in historyList" :key="index" class="history-item">
        {{ item.calculation }} = {{ item.result }}
      </li>
    </ul>
    <button @click="resetHistory" class="reset-button">Reset History</button>
  </div>
</template>

<script>
export default {
  props: ['historyList'],
  methods: {
    resetHistory() {
      this.$emit('resetHistory');
    }
  }
};
</script>

<style scoped>
h2 {
  text-align: center;
  margin-bottom: 20px;
}

ul {
  list-style-type: none;
  padding: 0;
  margin-bottom: 20px;
}

.history-item {
  padding: 10px;
  background-color: #f1f1f1;
  border: 1px solid #ddd;
  margin-bottom: 10px;
  border-radius: 5px;
}

.reset-button {
  padding: 10px 20px;
  background-color: #f44336;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.reset-button:hover {
  background-color: #d32f2f;
}
</style>