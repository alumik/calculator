<template>
  <div>
    <Button class="btn-secondary" caption="AC" @btnClick="btnClick"></Button>
    <Button class="btn-secondary" caption="+/-" @btnClick="btnClick"></Button>
    <Button class="btn-secondary" caption="%" @btnClick="btnClick"></Button>

    <Button class="btn-operator" caption="÷" @btnClick="btnClick"></Button>

    <Button class="btn-number" caption="7" @btnClick="btnClick"></Button>
    <Button class="btn-number" caption="8" @btnClick="btnClick"></Button>
    <Button class="btn-number" caption="9" @btnClick="btnClick"></Button>

    <Button class="btn-operator" caption="×" @btnClick="btnClick"></Button>

    <Button class="btn-number" caption="4" @btnClick="btnClick"></Button>
    <Button class="btn-number" caption="5" @btnClick="btnClick"></Button>
    <Button class="btn-number" caption="6" @btnClick="btnClick"></Button>

    <Button class="btn-operator" caption="-" @btnClick="btnClick"></Button>

    <Button class="btn-number" caption="1" @btnClick="btnClick"></Button>
    <Button class="btn-number" caption="2" @btnClick="btnClick"></Button>
    <Button class="btn-number" caption="3" @btnClick="btnClick"></Button>

    <Button class="btn-operator" caption="+" @btnClick="btnClick"></Button>

    <Button class="btn-large btn-number btn-bottom-left" caption="0" @btnClick="btnClick"></Button>
    <Button class="btn-number" caption="." @btnClick="btnClick"></Button>

    <Button class="btn-equal btn-bottom-right" caption="=" @btnClick="btnClick"></Button>
  </div>
</template>

<script>
import Button from '@/components/Button'
export default {
  name: 'Keypad',
  components: { Button },
  methods: {
    btnClick (btn) {
      this.$emit('btnClick', btn)
    }
  }
}
</script>

<style scoped>

  div {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    width: 100%;
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
