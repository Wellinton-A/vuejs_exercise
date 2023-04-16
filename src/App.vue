<script setup>
  import { computed } from '@vue/reactivity';
  import { reactive } from 'vue';

  const state = reactive ({
    number1: '',
    number2: '',
    signal: '+',
  })

  const result = computed(() => {
    const num1 = parseFloat(state.number1)
    const num2 = parseFloat(state.number2)
    if (isNaN(num1) || isNaN(num2)) {
      return ''
    }
    switch (state.signal) {
      case '+':
        return num1 + num2
      case '-':
      return num1 - num2
      case '*':
      return num1 * num2
      case '/':
      return num1 / num2
      default:
        return ''
    }
  })

  const isNotNumber1 = () => {
    const num1 = parseFloat(state.number1)
    if (isNaN(num1) && state.number1.length > 0) {
      return true
    }
  }

  const isNotNumber2 = () => {
    const num2 = parseFloat(state.number2)
    if (isNaN(num2) && state.number2.length > 0) {
      return true
    }
  }

</script>

<template>
  <div class="container text-bg-secondary mt-3 rounded-3">
    <h1>
      Calculator
    </h1>
  </div>
  <div class="container">
    <div class="group d-flex">
      <input :class="{isNotNumber:isNotNumber1()}" v-model="state.number1" type="text" class="form-control inp inp1">
      <select @change="evento => state.signal = evento.target.value" class="form-control select">
        <option value="+">+</option>
        <option value="-">-</option>
        <option value="*">x</option>
        <option value="/">÷</option>
      </select>
      <input :class="{isNotNumber:isNotNumber2()}" v-model="state.number2" type="text" class="form-control inp">
    </div>
    <div class="result">
      <span>Result: {{ result }}</span>
    </div>
  </div>

</template>

<style scoped>
.container {
  max-width: 400px;
  padding: 10px;
}

.inp {
  max-width: 100px;
  height: 60px;
  margin-left: 8px;
  margin-right: 8px;
}

.group {
  max-width: 350px;
  margin: 0 auto;
  justify-content: center;
}

.select {
  border: none;
  max-width: 70px;
  font-size: 30px;
  margin-left: initial;
}

.select:focus {
  border-color: transparent;
  box-shadow: none;
}

.inp1 {
  margin-right: 24px;
}

.result {
  text-align: center;
  margin-top: 40px;
  font-size: 32px;
}

.isNotNumber {
  outline-color: red;
  border-color: red;
}

.isNotNumber:focus {
  outline: 3px solid transparent;
  outline-color: red;
  border-color: red;
}
</style>
