<template>
    <div>
        <button class="row-line-button" 
        :class="{ clicked: isButtonActive }"
        @click="saveNumber(rowIndex)"><span>{{numberShown}}</span></button>
    </div>
</template>
<script>
export default {
  name: 'number-button-horizontal',
  components: {
  },
  props: {
    numberShown: Number,
    rowIndex: Number,
    numberAfterClick: Number,
    active: Boolean,
    isActiveLearn: Boolean,
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
    saveNumber(rowIndex) {
        if(this.numberShown > 0) {
            this.$emit('selected', rowIndex);
        }
    },
  }
}
</script>
<style lang="less">
.row-line-button {
  background-color: #feca57;
  border: none;
  color: white;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
  height: 7vh;
  width: 7vh;
  &.clicked {
    background-color: #ee5253;
  }
}
</style>