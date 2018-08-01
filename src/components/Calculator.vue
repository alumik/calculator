<template>
  <div>
    <TitleBar ref="title"></TitleBar>
    <Screen ref="screen" @keyBoardOn="keyBoardOn" @keyBoardOff="keyBoardOff" @keyPressed="keyPressed"></Screen>
    <Keypad @btnPressed="btnPressed"></Keypad>
  </div>
</template>

<script>
import TitleBar from '@/components/TitleBar'
import Screen from '@/components/Screen'
import Keypad from '@/components/Keypad'
export default {
  name: 'Calculator',
  components: { Keypad, Screen, TitleBar },
  data () {
    return {
      left: 0,
      operator: '',
      is_new_input: true
    }
  },
  methods: {
    btnPressed (button) {
      switch (button.type) {
        case 'btn-clear':
          this.btnClear()
          break
        case 'btn-changesign':
          this.btnChangeSign()
          break
        case 'btn-percentage':
          this.btnPercentage()
          break
        case 'btn-number':
          this.appendText(button.data)
          break
        case 'btn-operator':
          this.btnOperator(button.data)
          break
        case 'btn-equal':
          this.calculate()
          break
      }
    },

    keyPressed (e) {
      if ((e.key >= '0' && e.key <= '9') || e.key === '.') {
        this.appendText(e.key)
      } else if (e.key === '+' || e.key === '-') {
        this.btnOperator(e.key)
      } else if (e.key === '*') {
        this.btnOperator('×')
      } else if (e.key === '/') {
        this.btnOperator('÷')
      } else if (e.key === '%') {
        this.btnPercentage()
      } else if (e.key === 'Enter' || e.key === 'Return' || e.key === '=') {
        this.calculate()
      } else if (e.key === 'c' || e.key === 'C') {
        this.btnClear()
      } else if (e.key === '~') {
        this.btnChangeSign()
      }
    },

    btnClear () {
      // 只有在清除键为“AC”时才清除参数
      if (this.$refs.screen.$refs.input.value === 'AC') {
        this.resetArguments()
      }
      this.clearText()
    },

    btnPercentage () {
      if (this.$refs.screen.$refs.input.value !== 'ERROR') {
        this.$refs.screen.$refs.input.value = this.fixFloat(this.$refs.screen.$refs.input.value *= 0.01)
      }
    },

    btnChangeSign () {
      if (this.$refs.screen.$refs.input.value !== 'ERROR') {
        this.$refs.screen.$refs.input.value = this.fixFloat(this.$refs.screen.$refs.input.value *= -1)
      }
    },

    btnOperator (operator) {
      if (this.$refs.screen.$refs.input.value !== 'ERROR') {
        this.calculate()
        this.left = parseFloat(this.$refs.screen.$refs.input.value)
        this.operator = operator
        this.is_new_input = true
      }
    },

    clearText () {
      this.$refs.screen.$refs.input.value = 0
      this.$emit('setAllClearBtn')
    },

    appendText (number) {
      // 判断是否需要清空输入框
      if (this.is_new_input) {
        this.clearText()
        this.is_new_input = false
      }
      // 如果输入框中为0就把0覆盖掉
      if (this.$refs.screen.$refs.input.value === '0' && number !== '.') {
        this.$refs.screen.$refs.input.value = ''
      }
      // 如果有输入且不改变原来的0就把清除键设为“C”
      if (number !== '0') {
        this.$emit('setClearBtn')
      }
      // 设置只能输入一个小数点
      if (number === '.' && this.$refs.screen.$refs.input.value.indexOf('.') !== -1) {
        return
      }
      // 如果输入框中字符小于7个才能继续输入
      if (this.$refs.screen.$refs.input.value.length < 7) {
        this.$refs.screen.$refs.input.value += number
      }
    },

    calculate () {
      // 暂存右值
      let right = parseFloat(this.$refs.screen.$refs.input.value)

      // 尝试计算
      try {
        // 如果有运算符且不需要输入新值才计算
        if (this.operator !== '' && this.is_new_input !== true) {
          let answer
          switch (this.operator) {
            case '+':
              answer = this.left + right
              break
            case '-':
              answer = this.left - right
              break
            case '×':
              answer = this.left * right
              break
            case '÷':
              if (right === 0) {
                answer = 'ERROR'
              } else {
                answer = this.left / right
              }
              break
            default:
              answer = 'ERROR'
          }
          if (answer !== 'ERROR') {
            this.$refs.screen.$refs.input.value = this.fixFloat(answer)
          } else {
            this.$refs.screen.$refs.input.value = 'ERROR'
          }
          this.$emit('setAllClearBtn')
        }
      } catch (e) {
        this.$refs.screen.$refs.input.value = 'ERROR'
        this.$emit('setAllClearBtn')
      } finally {
        this.resetArguments()
      }
    },

    fixFloat (float) {
      float = float.toFixed(5)
      float.replace(/0+$/, '')
      return parseFloat(float)
    },

    resetArguments () {
      this.left = 0
      this.operator = ''
      this.is_new_input = true
    },

    keyBoardOn () {
      this.$refs.title.$refs.keyboardIndicator.setAttribute('style', 'color: #fff')
      this.$refs.title.$refs.keyboardIndicator.innerText = 'KEYBOARD ON'
      console.log(1)
    },

    keyBoardOff () {
      this.$refs.title.$refs.keyboardIndicator.setAttribute('style', 'color: #bbb')
      this.$refs.title.$refs.keyboardIndicator.innerText = 'KEYBOARD OFF'
    }
  },
  mounted () {
    this.clearText()
  }
}
</script>

<style scoped>
div {
  display: flex;
  box-sizing: border-box;
  margin: 100px auto;
  padding: 1px;
  width: 50%;
  max-width: 430px;
  min-width: 330px;
  border-radius: 10px;
  background-color: #999;
  /* 阴影效果来自 https://codepen.io/sdthornton/pen/wBZdXq */
  box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
  flex-direction: row;
  flex-wrap: wrap;
}
</style>
