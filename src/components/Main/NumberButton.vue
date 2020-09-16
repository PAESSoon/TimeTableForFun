<template>
    <div>
        <div @click="showNumber" :class="{ highlighted: highLightResult, blur:isActiveTestEnabled}" class="table-unit"><span>{{ numberShown }}</span></div>
    </div>
</template>
<script>
export default {
  name: 'number-button',
  components: {
  },
  props: {
    numberShown: Number,
    rowIndex: Number,
    columnIndex: Number,
    resultFromMultiplication: Number,
    columnNumberClicked: Number,
    rowNumberClicked: Number,
    isActiveLearn: Boolean,
    result: Number,
    columnRandom: Number,
    rowRandom: Number,
  },
  data() {
    return {
      isRowClickable: true,
      isColumnClickable: true,
      firstValue: 0,
      secondValue: 0,
    }
  },
  computed: {
    highLightResult() {
      if(this.isActiveLearn) {
        if(this.columnNumberClicked === this.rowIndex + 1 && this.rowNumberClicked === this.columnIndex + 1) {
          return true
        } 
      } else {
        if(this.numberShown === this.result && this.columnRandom === this.rowIndex + 1 && this.rowRandom === this.columnIndex + 1) {
          return true
        }
      }
      return false
    },
    isActiveTestEnabled() {
      if(this.columnRandom === this.rowIndex + 1 && this.rowRandom === this.columnIndex + 1) {
        return false
      } else if(this.isActiveTest) {
        return true
      }
      return false
    }
  },
  methods: {
    showNumber() {
      this.$emit('selected');
    },
    saveNumber() {
      if(this.isRowClickable && this.rowIndex === 0) {
        this.firstValue = this.columnIndex;
        this.isRowClickable = false;
      } else if(this.isColumnClickable && this.columnIndex === 0) {
        this.secondValue = this.rowIndex;
        this.isColumnClickable = false;
      }
    },
  }
}
</script>
<style lang="less">
.table-unit {
  background-color: #8395a7;
  border: none;
  text-align: center;
  line-height: 7vh;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
  height: 7vh;
  width: 7vh;
  &.highlighted {
    background-color: #5f27cd;
    transition: background-color 0.7s ease-in;
  }
  &.blur {
    background-color: #c8d6e5;
  }
  span {
    color: #c8d6e5;
  }
}
</style>