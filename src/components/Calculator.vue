<template>
  <div class="calculator">
    <TitleBar :keyboardIndicator="keyboardIndicator"></TitleBar>
    <Screen :screen="screen" @keyBoardOn="keyBoardOn" @keyBoardOff="keyBoardOff" @keyPressed="keyPressed"></Screen>
    <Keypad @btnClick="btnClick"></Keypad>
  </div>
</template>

<script>
import TitleBar from './TitleBar'
import Screen from './Screen'
import Keypad from './Keypad'

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
    btnClick (btn) {
      if ((btn >= '0' && btn <= '9') || btn === '.') {
        this.appendText(btn)
      } else if (btn === '+' || btn === '-' || btn === '×' || btn === '÷') {
        this.btnOperator(btn)
      } else if (btn === '%') {
        this.btnPercentage()
      } else if (btn === '=') {
        this.calculate()
      } else if (btn === 'C' || btn === 'AC') {
        this.btnClear()
      } else if (btn === '+/-') {
        this.btnChangeSign()
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
      if (this.clearButton === 'AC') {
        this.resetArguments()
      }
      this.clearText()
    },

    btnChangeSign () {
      if (this.screen !== 'ERROR') {
        this.screen = this.fixFloat(this.screen *= -1)
      }
    },

    btnPercentage () {
      if (this.screen !== 'ERROR') {
        this.screen = this.fixFloat(this.screen *= 0.01)
      }
    },

    // Number input
    appendText (number) {
      // Clear the screen if a new input is detected
      if (this.is_new_input) {
        this.clearText()
        this.is_new_input = false
      }
      // If the screen is 0 and the input is not a decimal, clear the screen
      if (this.screen === '0' && number !== '.') {
        this.screen = ''
      }
      // If the screen is not 0, change the clear button to 'C'
      if (number !== '0') {
        this.clearButton = 'C'
      }
      // If the input is a decimal and the screen already has a decimal, return
      if (number === '.' && this.screen.indexOf('.') !== -1) {
        return
      }
      // If the screen length is less than 7, append the number to the screen
      if (this.screen.length < 7) {
        this.screen += number
      }
    },

    btnOperator (operator) {
      if (this.screen !== 'ERROR') {
        this.calculate()
        this.left = parseFloat(this.screen)
        this.operator = operator
        this.is_new_input = true
      }
    },

    calculate () {
      // Store the value of the right side of the equation
      const right = parseFloat(this.screen)

      try {
        // If there is an operator and the input is not new
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

    fixFloat (float) {
      float = float.toFixed(5)
      float.replace(/0+$/, '')
      return parseFloat(float).toString()
    },

    clearText () {
      this.screen = '0'
      this.clearButton = 'AC'
    },

    resetArguments () {
      this.left = 0
      this.operator = ''
      this.is_new_input = true
    },

    keyBoardOn () {
      this.keyboardIndicator = true
    },

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
  .calculator {
    display: flex;
    box-sizing: border-box;
    margin: 100px auto;
    padding: 1px;
    width: 50%;
    max-width: 430px;
    min-width: 330px;
    border-radius: 10px;
    background-color: #999;
    box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
    flex-direction: row;
    flex-wrap: wrap;
  }
</style>
