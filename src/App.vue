<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
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
