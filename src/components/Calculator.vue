<template>
  <div class="calculator">
    <div class="display">
      <div class ="preview"> {{displayCal}}</div>
      {{current || '0'}}
    </div>
    <div @click="clear" class="btn operator2">C</div>
    <div @click="sign" class="btn operator2">+/-</div>
    <div @click="del" class="btn operator2">DEL</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiply" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
      displayCal : ''
    }
  },
  methods: {
    append(str) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${str}`;
      this.append_operation(str)
    },
    append_operation(str) {
      this.displayCal += str;
    },
    clear() {
      this.current = '';
      this.displayCal = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? 
        this.current.slice(1) : `-${this.current}`;
    },
    del() {
       this.current = this.current.substr(0,this.current.length - 1);
       this.displayCal = this.displayCal.substr(0,this.displayCal.length - 1);
    },
    dot() {
      if (this.current.indexOf('.') === -1 || this.previous.indexOf('.' === 1)) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.append_operation("/");
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    multiply() {
      this.append_operation("*");
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.append_operation("-");
      this.operator = (a, b) => a - b;


      this.setPrevious();
    },
    add() {
      this.append_operation("+");
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current), 
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    }
  }
}
</script>