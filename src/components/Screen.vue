<template>
  <input
    ref="input"
    @keypress="keyPressed"
    @focus="onFocus"
    @blur="onBlur"
    title="Screen"
    :value="screen"
    readonly="readonly"
  />
</template>

<script>
export default {
  name: 'Screen',
  props: {
    screen: {
      require: true
    }
  },
  methods: {
    onFocus () {
      this.$emit('keyBoardOn')
    },

    onBlur () {
      this.$emit('keyBoardOff')
    },

    keyPressed (e) {
      this.$emit('keyPressed', e)
    }
  }
}
</script>

<style scoped>
  @font-face{
    font-weight: normal;
    font-style: normal;
    font-family: 'helvetica_neue_ultralight';
    src: url('../assets/fonts/helveticaneue-ultralight-webfont.eot');
    src: url('../assets/fonts/helveticaneue-ultralight-webfont.eot') format('embedded-opentype'),
    url('../assets/fonts/helveticaneue-ultralight-webfont.woff') format('woff'),
    url('../assets/fonts/helveticaneue-ultralight-webfont.ttf') format('truetype'),
    url('../assets/fonts/helveticaneue-ultralight-webfont.svg') format('svg');
  }

  input {
    box-sizing: border-box;
    padding: 35px 30px 25px;
    width: 100%;
    height: 120px;
    border-style: none;
    background-color: transparent;
    color: #fff;
    text-align: right;
    font-size: 84px;
    font-family: 'helvetica_neue_ultralight', Helvetica, Arial, sans-serif;
  }
</style>
