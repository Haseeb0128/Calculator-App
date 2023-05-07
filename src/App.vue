<template>
  <div class="d-flex justify-content-center align-items-center flex-column mt-5">
    <h1>Calculator App</h1>
    <div class="container m-5 p-3">
      <!-- Calculator Result -->
      <div class="display p-3 fs-4">{{ calculatorValue || 0 }}</div>
      <!-- Calculator buttons -->
      <div class="row no-gutters mt-3">
        <div class="col-3 d-flex flex-column" v-for="n in calculatorElements" :key="n">
          <button class="btn btn-light m-1" :class="{ 'btn btn-dark': ['AC', '/', '*', '%', '-', '+', '='].includes(n) }"
            @click="action(n)">{{ n
            }}</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      calculatorValue: '',
      calculatorElements: ['AC', '*', '/', '-', 7, 8, 9, '+', 4, 5, 6, '%', 1, 2, 3, '=', 0, '.'],
      operator: null,
      previousCalculatorValue: '',
    }
  },
  methods: {
    action(n) {
      // Append Value or conversion of numeric value to string for display
      if (!isNaN(n) || n === '.') {
        this.calculatorValue += n + '';
      }

      // Clear Value
      if (n === 'AC') {
        this.calculatorValue = '';
      }

      // Percentage calculation
      if (n === '%') {
        this.calculatorValue = this.calculatorValue / 100 + '';
      }


      if (['/', '+', '-', '*'].includes(n)) {
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = '';
      }


      if (n === '=') {
        // The eval function evaluates an expression, even if the expression is a string
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        );
        this.previousCalculatorValue = '';
        this.operator = null;
      }
    }
  }
}
</script>

<style>
.container {
  max-width: 400px;
  background-color: gray;
}

.display {
  background-color: silver;
}
</style>