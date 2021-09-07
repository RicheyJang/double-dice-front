<template>
  <div class="group">
    <div class="inner-dice">
      <rand-dice :cell-number="diceNum1"></rand-dice>
      <rand-dice :cell-number="diceNum2"></rand-dice>
    </div>
    <h1 class="inner-num">
      {{ sumNum }}
    </h1>
    <button class="inner-button" @click="rollDice" :disabled="isRolling">
      <span>扔</span>
    </button>
  </div>
</template>

<script>
import RandDice from "@/components/RandDice";

function randomNum(minNum,maxNum){
  switch(arguments.length){
    case 1:
      return parseInt(Math.random()*minNum+1,10);
    case 2:
      return parseInt(Math.random()*(maxNum-minNum+1)+minNum,10);
    default:
      return 0;
  }
}

export default {
  name: "DoubleDice",
  components: {RandDice},
  data() {
    return {
      diceNum1: 1,
      diceNum2: 1,
      interID: 0,
      isRolling: false
    }
  },
  props: {
    maxRollTime: {
      default: 6,
      type: Number
    }
  },
  computed: {
    sumNum() {
      return this.diceNum1 + this.diceNum2;
    }
  },
  methods: {
    rollDice() {
      this.isRolling = true;
      const vm = this;
      let rollTime = 0;
      this.interID = setInterval(function (){
        vm.diceNum1 = randomNum(1,6);
        vm.diceNum2 = randomNum(1,6);
        rollTime++;
        if(rollTime>=vm.maxRollTime){
          vm.stopDice();
        }
      }, 80);
    },
    stopDice() {
      clearInterval(this.interID);
      this.isRolling = false;
    }
  }
}
</script>

<style lang="scss" scoped>
$sumFontSize : 70px;
$buttonRadius : 15px;

.group {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;

  background-color: #333;

  display: flex;

  flex-direction: column;
  justify-content: space-around;
  //align-items: space-around;

  .inner-dice {
    display: flex;

    justify-content: space-around;
    align-items: center;
  }

  .inner-num {
    font-size: $sumFontSize;
    color: #F0F0F0;
  }

  .inner-button {
    width:40%;
    min-height: 10%;

    margin-left:auto;
    margin-right: auto;
    text-align:center;

    background-color: #f0f0f0;
    box-shadow: 0 6px #999; /*下阴影*/

    border: 0px;
    -moz-border-radius: $buttonRadius;/*圆角*/
    -webkit-border-radius: $buttonRadius;
    border-radius: $buttonRadius;

    span { // 文字
      font-size: 8vh;
      cursor: pointer;
      display: inline-block;
      position: relative;
      transition: 0.4s;
    }
    span:after {
      content: '！';
      position: absolute;
      opacity: 0;
      top: 0;
      right: -3vh;
      transition: 0.4s;
    }
  }
  .inner-button:active { /*按下*/
    background-color: #cacaca;
    box-shadow: 0 2px #666;
    transform: translateY(4px);
  }
  .inner-button:hover { /*鼠标放置*/
    background-color: #cacaca;

    span {
      padding-right: 7vh;
    }
    span:after {
      opacity: 1;
      right: 0;
    }
  }
}
</style>