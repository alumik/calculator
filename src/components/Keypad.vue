<template>
  <div>
    <button class="btn-secondary" @click="btnClear()">AC</button>
    <button class="btn-secondary" @click="btnChangeSign()">+/-</button>
    <button class="btn-secondary" @click="btnPercentage()">%</button>

    <button class="btn-operator" @click="btnOperator('÷')">÷</button>

    <button class="btn-number" @click="btnNumber('7')">7</button>
    <button class="btn-number" @click="btnNumber('8')">8</button>
    <button class="btn-number" @click="btnNumber('9')">9</button>

    <button class="btn-operator" @click="btnOperator('×')">×</button>

    <button class="btn-number" @click="btnNumber('4')">4</button>
    <button class="btn-number" @click="btnNumber('5')">5</button>
    <button class="btn-number" @click="btnNumber('6')">6</button>

    <button class="btn-operator" @click="btnOperator('-')">-</button>

    <button class="btn-number" @click="btnNumber('1')">1</button>
    <button class="btn-number" @click="btnNumber('2')">2</button>
    <button class="btn-number" @click="btnNumber('3')">3</button>

    <button class="btn-operator" @click="btnOperator('+')">+</button>

    <button class="btn-large btn-number btn-bottom-left" @click="btnNumber('0')">0</button>
    <button class="btn-number" @click="btnNumber('.')">.</button>

    <button class="btn-equal btn-bottom-right" @click="btnEqual()">=</button>
  </div>
</template>

<script>
export default {
  name: 'Keypad',
  methods: {
    btnClear () {
      this.$emit('btnPressed', { type: 'btn-clear' })
    },

    btnChangeSign () {
      this.$emit('btnPressed', { type: 'btn-changesign' })
    },

    btnPercentage () {
      this.$emit('btnPressed', { type: 'btn-percentage' })
    },

    btnNumber (number) {
      this.$emit('btnPressed', { type: 'btn-number', data: number })
    },

    btnOperator (operator) {
      this.$emit('btnPressed', { type: 'btn-operator', data: operator })
    },

    btnEqual () {
      this.$emit('btnPressed', { type: 'btn-equal' })
    }
  }
}
</script>

<style scoped>
  @font-face{
    font-weight: normal;
    font-style: normal;
    font-family: 'helvetica_neue';
    src: url('../assets/fonts/helveticaneue-webfont.eot');
    src: url('../assets/fonts/helveticaneue-webfont.eot') format('embedded-opentype'),
    url('../assets/fonts/helveticaneue-webfont.woff') format('woff'),
    url('../assets/fonts/helveticaneue-webfont.ttf') format('truetype'),
    url('../assets/fonts/helveticaneue-webfont.svg') format('svg');
  }

  div {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    width: 100%;
  }

  button {
    margin: 1px;
    height: 80px;
    border-style: none;
    text-align: center;
    font-family: 'helvetica_neue', Helvetica, Arial, sans-serif;
    cursor: pointer;
    flex: 1 1 24%;
  }

  button:focus {
    outline: none;
  }

  .btn-operator, .btn-equal {
    background-color: #f69232;
    color: #fff;
    font-size: 48px;
    font-family: "Courier New", Courier, monospace;
  }

  .btn-operator:active, .btn-equal:active {
    background-color: #ba7737;
    color: #000;
  }

  .btn-secondary {
    background-color: #d6d6d6;
    font-size: 32px;
  }

  .btn-secondary:active {
    background-color: #a9a9a9;
  }

  .btn-number {
    background-color: #e0e0e0;
    font-size: 36px;
  }

  .btn-number:active {
    background-color: #b2b2b2;
  }

  .btn-large {
    padding-right: calc(24% + 8px);
    flex: 1 1 49%;
  }

  .btn-bottom-left {
    border-radius: 0 0 0 9px;
  }

  .btn-bottom-right {
    border-radius: 0 0 9px 0;
  }
</style>
