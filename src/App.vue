<template>
  <div id="app">
    <Calculator/>
  </div>
</template>

<script>
import Calculator from './components/Calculator'

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
  }

  body {
    background-color: #f5f5f5;
    user-select: none;
  }
</style>
