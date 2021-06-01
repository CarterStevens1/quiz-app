<template>
  <div class="app">
    <h1>Math Quiz App</h1>

    <operator-quiz
      @onBack="clearOperator"
      v-if="operator"
      :operator="operator"
    />
    <operatorSelector v-if="!operator" @selectOperator="selectOperator" />
  </div>
</template>

<script>
import operatorSelector from "./components/operatorSelector.vue";
import operatorQuiz from "./components/operatorQuiz.vue";
export default {
  name: "App",
  data() {
    return {
      operator: null,
    };
  },
  methods: {
    selectOperator(operator) {
      this.operator = operator;
    },
    clearOperator() {
      this.operator = null;
    },
  },

  components: {
    operatorSelector,
    operatorQuiz,
  },
};
</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 24px;
}

button {
  padding: 10px;
  width: 200px;
  height: 80px;
  margin-right: 10px;
  background-color: #10aeb2;
  color: #fff;
  font-size: 24px;
  cursor: pointer;
  vertical-align: top;
  border: none;
}
</style>
