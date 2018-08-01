<template>
  <div>
    <div class="btn-round btn-round-red"></div>
    <div class="btn-round btn-round-yellow"></div>
    <div class="btn-round btn-round-green"></div>
    <div ref="keyboardIndicator" id="keyboard-indicator">KEYBOARD OFF</div>
  </div>
</template>

<script>
export default {
  name: 'TitleBar'
}
</script>

<style scoped>
  div {
    box-sizing: border-box;
    display: flex;
    width: 100%;
    box-shadow: none;
    margin: 0;
  }

  .btn-round {
    margin-top: 10px;
    margin-left: 15px;
    width: 20px;
    height: 20px;
    border-radius: 50%;
  }

  .btn-round-red {
    background-color: #fe534d;
  }

  .btn-round-yellow {
    background-color: #ffbf2f;
  }

  .btn-round-green {
    background-color: #28c93f;
  }

  .btn-round-red:active {
    background-color: #cd4c46;
  }

  .btn-round-yellow:active {
    background-color: #cd962f;
  }

  .btn-round-green:active {
    background-color: #219732;
  }

  #keyboard-indicator {
    display: inline-block;
    margin: 10px 15px 0 0;
    color: #bbb;
    text-align: right;
    font-weight: bold;
    font-size: 18px;
    flex: 1 0;
  }
</style>
