<template>
  <div>
    <TitleBar :keyboardIndicator="keyboardIndicator"></TitleBar>
    <Screen :screen="screen" @keyBoardOn="keyBoardOn" @keyBoardOff="keyBoardOff" @keyPressed="keyPressed"></Screen>
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
      is_new_input: true,
      screen: '0',
      clearButton: 'AC',
      keyboardIndicator: false
    }
  },
  methods: {
    // 屏幕按键按下
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

    // 实体按键按下
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

    // C/AC键功能
    btnClear () {
      // 只有在清除键为“AC”时才清除参数
      if (this.clearButton === 'AC') {
        this.resetArguments()
      }
      this.clearText()
    },

    // +/-键功能
    btnChangeSign () {
      if (this.screen !== 'ERROR') {
        this.screen = this.fixFloat(this.screen *= -1)
      }
    },

    // 百分号键功能
    btnPercentage () {
      if (this.screen !== 'ERROR') {
        this.screen = this.fixFloat(this.screen *= 0.01)
      }
    },

    // 数字键和小数点键功能
    appendText (number) {
      // 判断是否需要清空输入框
      if (this.is_new_input) {
        this.clearText()
        this.is_new_input = false
      }
      // 如果输入框中为0就把0覆盖掉
      if (this.screen === '0' && number !== '.') {
        this.screen = ''
      }
      // 如果有输入且不改变原来的0就把清除键设为“C”
      if (number !== '0') {
        this.clearButton = 'C'
      }
      // 设置只能输入一个小数点
      if (number === '.' && this.screen.indexOf('.') !== -1) {
        return
      }
      // 如果输入框中字符小于7个才能继续输入
      if (this.screen.length < 7) {
        this.screen += number
      }
    },

    // 运算符键功能
    btnOperator (operator) {
      if (this.screen !== 'ERROR') {
        this.calculate()
        this.left = parseFloat(this.screen)
        this.operator = operator
        this.is_new_input = true
      }
    },

    // 进行计算
    calculate () {
      // 暂存右值
      let right = parseFloat(this.screen)

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
            this.screen = this.fixFloat(answer)
          } else {
            this.screen = 'ERROR'
          }
          this.clearButton = 'AC'
        }
      } catch (e) {
        this.screen = 'ERROR'
        this.clearButton = 'AC'
      } finally {
        this.resetArguments()
      }
    },

    // 修复浮点精度问题
    fixFloat (float) {
      float = float.toFixed(5)
      float.replace(/0+$/, '')
      return parseFloat(float).toString()
    },

    // 清空显示屏
    clearText () {
      this.screen = '0'
      this.clearButton = 'AC'
    },

    // 重置参数
    resetArguments () {
      this.left = 0
      this.operator = ''
      this.is_new_input = true
    },

    // 键盘输入打开
    keyBoardOn () {
      this.keyboardIndicator = true
    },

    // 键盘输入关闭
    keyBoardOff () {
      this.keyboardIndicator = false
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
    box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
    flex-direction: row;
    flex-wrap: wrap;
  }
</style>
