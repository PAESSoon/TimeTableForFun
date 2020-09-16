<template>
    <div>
        <button class="column-line-button" @click="saveNumber(numberShown)" :class="{active: isButtonActive}"><span v-if="numberShown > 0">{{numberShown}}</span></button>
    </div>
</template>
<script>
export default {
  name: 'number-button-horizontal',
  components: {
  },
  props: {
    numberShown: Number,
    columnIndex: Number,
    active: Boolean,
    isActiveLearn: Boolean,
    isActiveTest: Boolean,
    randomNumber: Number,
  },
  data() {
    return {
      firstValue: 0,
      secondValue: 0,
    }
  },
  computed: {
    isButtonActive() {
      if(this.isActiveLearn) {
        return this.active
      }
      else if(!this.isActiveLearn && this.numberShown === this.randomNumber) {
        return true
      }
      else {
        return false
      }
    }
  },
  methods: {
    saveNumber(numberShown) {
      console.log('this is numberShown from child', numberShown);
      if(this.isActiveLearn && this.numberShown > 0) {
        this.$emit('selected', numberShown);
      }
    },
  }
} 
</script>
<style lang="less">
.column-line-button {
  background-color: #ff9f43;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
  height: 7vh;
  width: 7vh;
  &.active {
    background-color: #ee5253;
  }
}
</style>