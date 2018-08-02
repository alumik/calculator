<template>
  <button @click="btnClick">{{ caption }}</button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    caption: {
      require: true
    }
  },
  methods: {
    btnClick () {
      this.$emit('btnClick', this.caption)
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
</style>
