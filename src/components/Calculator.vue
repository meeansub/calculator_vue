<template>
  <div class="calculator">
      <div class="display">
          {{current || '0'}}
        </div>
      <div @click="clear" class="btn other">AC</div>
      <div @click="sign" class="btn other">+/-</div>
      <div @click="del" class="btn other">DEL</div>
      <div @click="append('/')" class="btn operator">/</div>
      <div @click="append('7')" class="btn">7</div>
      <div @click="append('8')" class="btn">8</div>
      <div @click="append('9')" class="btn">9</div>
      <div @click="append('*')" class="btn operator">*</div>
      <div @click="append('4')" class="btn">4</div>
      <div @click="append('5')" class="btn">5</div>
      <div @click="append('6')" class="btn">6</div>
      <div @click="append('-')" class="btn operator">-</div>
      <div @click="append('1')" class="btn">1</div>
      <div @click="append('2')" class="btn">2</div>
      <div @click="append('3')" class="btn">3</div>
      <div @click="append('+')" class="btn operator">+</div>
      <div @click="append('0')" class="btn zero">0</div>
      <div @click="dot" class="btn">.</div>
      <div @click="equal" class="btn operator">=</div>

  </div>
</template>

<script>
export default {
    data() {
        return {
            current : '',
            operator : null,
            operatorClicked : false,
        }
    },
    methods : {
        clear() {
            this.current = '';
        },
        sign() {
            this.current = this.current.charAt(0) === '-' ?
                this.current.slice(1) : `-${this.current}`;
        },
        del() {
            this.current = this.current.substr(0,this.current.length - 1);
        },
        append(str) {
            if(this.operatorClicked) {
                this.current = '';
                this.operatorClicked = false;
            }
            this.current = `${this.current}${str}`;
        },
        dot() {
            if(this.current.indexOf('.') === -1) {
                this.append('.');
            }
        },
        equal() {
            /*여기에 eval 함수 넣기*/
            this.current = `${eval(this.current)}`;
        },
    }
}
</script>

<style>
    .calculator {
        margin: 0 auto;
        width: 400px;
        font-size: 30px;
        border: 1px solid #333;
        display: grid;
        grid-template: repeat(4, 1fr);
        grid-auto-rows: minmax(50px, auto);
        vertical-align: middle;
    }

    .display {
        grid-column: 1 / 5;
        background-color:black;
        color: white;
    }

    .zero {
        grid-column: 1 / 3;
    }

    .btn {
        background-color : grey;
        border: 1px solid;
    }

    .operator {
        background-color:salmon;
    }

    .other {
        background-color: lightgray;
    }

</style>