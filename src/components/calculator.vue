<template>
  <td>
    <div class="container">
      <div class="calc-body">
        <div class="calculator">
          <div class="calc-screen">
            <div class="calculator_display">{{display}}</div>
          </div>
          <div class="calculator_key">
            <table>
              <tr>
                <td>
                  <button class="key-operator button" @click="add">+</button>
                </td>
                <td>
                  <button class="key-operator button" @click="sub">-</button>
                </td>
                <td>
                  <button class="key-operator button" @click="multiply">*</button>
                </td>
                <td>
                  <button class="key-operator button" @click="divide">/</button>
                </td>
              </tr>
              <tr>
                <td>
                  <button class="button" @click="append(7)">7</button>
                </td>
                <td>
                  <button class="button" @click="append(8)">8</button>
                </td>
                <td>
                  <button class="button" @click="append(9)">9</button>
                </td>
                <td rowspan="4">
                  <button
                    class="button key--equal calc-equal-but"
                    data-action="calculate"
                    @click="equal"
                  >=</button>
                </td>
              </tr>
              <tr>
                <td>
                  <button class="button" @click="append(7)">4</button>
                </td>
                <td>
                  <button class="button" @click="append(5)">5</button>
                </td>
                <td>
                  <button class="button" @click="append(6)">6</button>
                </td>
              </tr>
              <tr>
                <td>
                  <button class="button" @click="append(1)">1</button>
                </td>
                <td>
                  <button class="button" @click="append(2)">2</button>
                </td>
                <td>
                  <button class="button" @click="append(3)">3</button>
                </td>
              </tr>
              <tr class="calc-button-row1">
                <td>
                  <button class="button" @click="append(0)">0</button>
                </td>
                <td>
                  <button class="button" @click="decimal">.</button>
                </td>
                <td>
                  <button class="button" @click="clear">AC</button>
                </td>
              </tr>
            </table>
          </div>
        </div>
      </div>
    </div>
  </td>
</template>
<style scoped>
* {
  box-sizing: border-box;
  font-family: "Roboto", sans-serif;
}

.calculator_key {
  display: grid;
}

* {
  box-sizing: border-box;
  font-family: "Roboto", sans-serif;
}

body {
  background: #3a4655;
}

.container {
  width: 400px;
  margin: auto;
}

.calc-body {
  width: 275px;
  margin: auto;
  min-height: 400px;
  border: solid 1px #3a4655;
  box-shadow: 0 8px 50px -7px black;
}

.calc-screen {
  background: #3a4655;
  width: 100%;
  height: 150px;
  padding: 20px;
  color: #e0b612;
  text-align: -webkit-right;
  font-size: 40px;
}

.is-depressed {
  background-color: #aeb3ba !important;
}

.calc-operation {
  text-align: right;
  color: #727b86;
  font-size: 21px;
  padding-bottom: 10px;
  border-bottom: dotted 1px;
}

.calc-typed {
  margin-top: 20px;
  font-size: 45px;
  text-align: right;
  /* color: #fff; */
}

.calc-button-row {
  width: 100%;
  background: #3c4857;
}

.calc-equal-but {
  height: 304px;
}

.button {
  width: 66px;
  background: #425062;
  color: #fff;
  padding: 20px;
  display: inline-block;
  font-size: 25px;
  text-align: center;
  vertical-align: middle;
  margin-right: -4px;
  border-right: solid 2px #3c4857;
  border-bottom: solid 2px #3c4857;
  transition: all 0.2s ease-in-out;
}

.button.l {
  color: #aeb3ba;
  background: #404d5e;
}

.button.c {
  color: #d95d4e;
  background: #404d5e;
}

.button:hover {
  /* background: #E0B612; */
  transform: rotate(5deg);
}

.button.c:hover,
.button.l:hover {
  background: #e0b612;
  color: #fff;
}

.blink-me {
  color: #e0b612;
}
</style>
<script>
export default {
  name: "calculator",
  data() {
    return {
      display: 0,
      operatorClicked: false,
      previous: null,
      operator: null
    };
  },
  methods: {
    clear() {
      this.display = 0;
    },
    append(num) {
      if (this.operatorClicked == true) {
        this.display = "";
        this.operatorClicked == false;
      }
      this.display = this.display === 0 ? num : "" + this.display + num;
    },
    add() {
      this.operator = (a, b) => a + b;
      this.previous = this.display;
      this.operatorClicked = true;
    },
    sub() {
      this.operator = (a, b) => a - b;
      this.previous = this.display;
      this.operatorClicked = true;
    },
    decimal() {
      if (this.display.indexOf(".") === -1) {
        this.append(".");
      }
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.previous = this.display;
      this.operatorClicked = true;
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.previous = this.display;
      this.operatorClicked = true;
    },
    equal() {
      this.display = this.operator(Number(this.previous), Number(this.display));
      this.previous = "";
      this.operatorClicked = false;
    }
  }
};
</script>