<template>
  <div class="box" v-bind:class="className" v-html="cellHtml"></div>
</template>

<script>
export default {
  name: 'RandDice',
  props: {
    cellNumber: Number
  },
  computed:{
    numberNum:function(){
      let old = parseInt(this.cellNumber);
      if(old < 1){
        old = 1;
      }
      if(old > 6){
        old = 6;
      }
      return old;
    },
    className:function(){
      return 'cell' + this.numberNum
    },
    cellHtml:function(){
      let returnHtml = '';
      switch (this.numberNum) {
        case 1:returnHtml = '<i></i>';break;
        case 2:returnHtml = '<i></i><i></i>';break;
        case 3:returnHtml = '<i></i><i></i><i></i>';break;
        case 4:returnHtml = '<div><i></i><i></i></div><div><i></i><i></i></div>';break;
        case 5:returnHtml = '<div><i></i><i></i></div><div><i></i></div><div><i></i><i></i></div>';break;
        case 6:returnHtml = '<div><i></i><i></i></div><div><i></i><i></i></div><div><i></i><i></i></div>';break;
      }
      return returnHtml;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
$diceSize : 25vw;
$maxDiceSize : 25vh;
$dotSize : 5vw;
$maxDotSize : 5vh;

.box{
  height: $diceSize;
  width: $diceSize;
  max-width: $maxDiceSize;
  max-height: $maxDiceSize;
  /* box: */
  background: #F0F0F0;
  box-shadow: 0 2px 20px 0 rgba(0,0,0,0.05), 0 5px 10px 0 rgba(0,0,0,0.10), inset 0 0 0 5px rgba(203,203,203,0.50);
  border-radius: 20px;
  display: flex;
  padding: 5vw;

  i{
    display: block;
    height: $dotSize;
    width: $dotSize;
    max-height: $maxDotSize;
    max-width: $maxDotSize;
    border-radius: 50%;
    background-image: linear-gradient(-135deg, #737373 0%, #3B3B3B 100%);
    box-shadow: 0 1px 1px 1px rgba(255,255,255,0.50), inset 0 1px 3px 0 rgba(0,0,0,0.50);
  }

  &.cell1{
    justify-content: center;
    align-items: center;
    i{
      height: 7vw;
      width: 7vw;
      /* Oval Copy: */
      background-image: linear-gradient(-135deg, #FF7E7E 0%, #FF0000 100%);
      box-shadow: 0 1px 1px 1px rgba(255,255,255,0.50), inset 0 1px 3px 0 rgba(0,0,0,0.50);
    }
  }

  &.cell2{
    justify-content: space-between;
    i{
      &:nth-child(2){
        align-self: flex-end;
      }
    }
  }

  &.cell3{
    justify-content: space-between;
    i{
      &:nth-child(2){
        align-self: center;
      }
      &:nth-child(3){
        align-self: flex-end;
      }
    }
  }

  &.cell4{
    flex-direction: column;
    justify-content: space-between;
    div{
      display: flex;
      flex-direction: row;
      justify-content: space-between;
    }
  }

  &.cell5{
    flex-direction: column;
    justify-content: space-between;
    div{
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      &:nth-child(2){
        justify-content: center;
      }
    }
  }

  &.cell6{
    flex-direction: column;
    justify-content: space-between;
    div{
      display: flex;
      flex-direction: row;
      justify-content: space-between;
    }
  }
}
</style>
