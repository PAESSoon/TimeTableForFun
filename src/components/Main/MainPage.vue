
<template>
    <div class="multiplication-main-container">
        <div class="scrollContainer">
            <div class="options">
                <button @click="activateLearnMode" class="option-learn" :class="{ activateLearn: activeLearn }">Learn</button>
                    <button @click="activateTestMode" class="test">Test</button>
                <div class="change-table-size"> 
                    <div class="arrow" @click="decrease">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 492 492" width="16" height="16"><path d="M198.608 246.104L382.664 62.04c5.068-5.056 7.856-11.816 7.856-19.024 0-7.212-2.788-13.968-7.856-19.032l-16.128-16.12C361.476 2.792 354.712 0 347.504 0s-13.964 2.792-19.028 7.864L109.328 227.008c-5.084 5.08-7.868 11.868-7.848 19.084-.02 7.248 2.76 14.028 7.848 19.112l218.944 218.932c5.064 5.072 11.82 7.864 19.032 7.864 7.208 0 13.964-2.792 19.032-7.864l16.124-16.12c10.492-10.492 10.492-27.572 0-38.06L198.608 246.104z" fill="#0abde3"/></svg>
                    </div>
                    <div class="input-width">{{ number }}</div>
                    <div class="arrow" @click="increase">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 492 492" width="16" height="16"><path d="M382.678 226.804L163.73 7.86C158.666 2.792 151.906 0 144.698 0s-13.968 2.792-19.032 7.86l-16.124 16.12c-10.492 10.504-10.492 27.576 0 38.064L293.398 245.9l-184.06 184.06c-5.064 5.068-7.86 11.824-7.86 19.028 0 7.212 2.796 13.968 7.86 19.04l16.124 16.116c5.068 5.068 11.824 7.86 19.032 7.86s13.968-2.792 19.032-7.86L382.678 265c5.076-5.084 7.864-11.872 7.848-19.088.016-7.244-2.772-14.028-7.848-19.108z" fill="#0abde3"/></svg>
                    </div>
                </div>
            </div>
                <div class="main-instruction">
                    <div class="instruction"> Score 5 in a row! </div>
                    <div class="result-score">
                        <span class="multiplying-numbers" v-if="randomNumberColumn !== undefined">
                            {{ randomNumberColumn }} X {{ randomNumberRow }}
                            </span>
                        <div class="user-input">
                            <div class="input-side">
                                <input @click="runAgain" @keyup.enter="checkResult" v-model="userInput" ref="userInput" :disabled="isInputDisabled" :placeholder="[placeholderEdited]" class="result-input" :class="{correctInput: isCorrectInput}">
                                <button @click="runTest" class="run-test" :class="{ isClickable: clickable }">New Test</button>
                                <div class="countdown">{{ countDown }}</div>
                            </div>
                        </div>
                        <div class="score">
                            <span>Score:</span>
                            <div class="show-scores">
                                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 368 368" width="12" height="12">
                                <path d="M261.336 226.04c-3.296-2.952-8.36-2.664-11.296.624C233.352 245.312 209.288 256 184 256c-25.28 0-49.352-10.688-66.04-29.336-2.952-3.288-8-3.576-11.296-.624-3.296 2.944-3.568 8-.624 11.296C125.76 259.368 154.176 272 184 272c29.832 0 58.248-12.64 77.96-34.664 2.944-3.296 2.664-8.352-.624-11.296z"/>
                                <path d="M184 0C82.544 0 0 82.544 0 184s82.544 184 184 184 184-82.544 184-184S285.456 0 184 0zm0 352c-92.64 0-168-75.36-168-168S91.36 16 184 16s168 75.36 168 168-75.36 168-168 168z"/>
                                <path d="M248 128c-22.056 0-40 17.944-40 40 0 4.416 3.584 8 8 8s8-3.584 8-8c0-13.232 10.768-24 24-24s24 10.768 24 24c0 4.416 3.584 8 8 8s8-3.584 8-8c0-22.056-17.944-40-40-40zM144 168c0 4.416 3.584 8 8 8s8-3.584 8-8c0-22.056-17.944-40-40-40s-40 17.944-40 40c0 4.416 3.584 8 8 8s8-3.584 8-8c0-13.232 10.768-24 24-24s24 10.768 24 24z"/>
                                </svg>
                                <div class="good-answer">{{ goodAnswerCount }}</div>
                                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 368 368" width="12" height="12">
                                <path d="M184 0C82.544 0 0 82.544 0 184s82.544 184 184 184c101.464 0 184-82.544 184-184S285.464 0 184 0zm0 352c-92.64 0-168-75.36-168-168S91.36 16 184 16c92.632 0 168 75.36 168 168s-75.368 168-168 168z"/>
                                <path d="M144 152c0-13.232-10.768-24-24-24s-24 10.768-24 24 10.768 24 24 24 24-10.768 24-24zm-32 0c0-4.408 3.592-8 8-8s8 3.592 8 8-3.592 8-8 8-8-3.592-8-8zM248 128c-13.232 0-24 10.768-24 24s10.768 24 24 24 24-10.768 24-24-10.768-24-24-24zm0 32c-4.416 0-8-3.592-8-8s3.584-8 8-8 8 3.592 8 8-3.584 8-8 8zM184 224c-29.824 0-58.24 12.632-77.96 34.664-2.944 3.296-2.664 8.352.624 11.296a7.998 7.998 0 0011.296-.624C134.648 250.688 158.72 240 184 240c25.28 0 49.352 10.688 66.04 29.336A7.963 7.963 0 00256 272a7.966 7.966 0 005.336-2.04c3.288-2.944 3.568-8 .624-11.296C242.24 236.64 213.832 224 184 224z"/>
                                </svg>
                                <div class="wrong-answer">{{ wrongAnswerCount }}</div>
                            </div>
                        </div>
                    </div>
                </div>
            <div class="main-page">
                <div class="first-column">
                    <div class="first-column-item" v-for="(item, index) in firstRowArray" :key="index">
                        <number-button-vertical
                            class="number-button-column"
                            :active="(numberFromRow < 1 &&  multiplicationResult === 0) || (numberFromRow > 0 &&  multiplicationResult > 0)"
                            :numberShown="item"
                            :columnIndex="index"
                            :isActiveLearn="activeLearn"
                            :randomNumber="randomNumberColumn"
                            @selected="findItemColumn($event)"
                        >
                        </number-button-vertical>
                    </div>
                </div>
            
                <div class="center-panel">
                    <div class="first-row">
                        <div class="first-row-item" v-for="(item, index) in firstRowArray.slice(1)" :key="index">
                            <number-button-horizontal
                                class="number-button-row"
                                :active="(numberFromColumn < 1 &&  multiplicationResult === 0) || (numberFromColumn > 0 &&  multiplicationResult > 0)"
                                :numberShown="item"
                                :rowIndex="index"
                                :isActiveLearn="activeLearn"
                                :randomNumber="randomNumberRow"
                                :numberAfterClick="numberFromRow"
                                @selected="findItemRow($event);"
                            >
                            </number-button-horizontal>
                        </div>               
                    </div>

                    <div class="table">
                        <div class="single-row" v-for="(row, mainIndex) in resultArray" :key="mainIndex">
                            <div class="single-item" v-for="(item, index) in row" :key="index">
                                <number-button
                                    class="number-button"
                                    :numberShown="item"
                                    :rowIndex="mainIndex"
                                    :columnIndex="index"
                                    :isActiveLearn="activeLearn"
                                    :randomNumber="randomNumberRow"
                                    :resultFromMultiplication="multiplicationResult"
                                    :columnNumberClicked="numberFromColumn"
                                    :rowNumberClicked="numberFromRow"
                                    :result="resultNumber"
                                    :columnRandom="randomNumberColumn"
                                    :rowRandom="randomNumberRow"
                                >
                                </number-button>
                            </div>  
                        </div>
                    </div>
                </div>
            </div>  
        </div>  
        <footer>
            <div class="footer" :style="addMargin">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" width="12" height="12">
                <path d="M437.02 74.981C388.668 26.629 324.38 0 256 0S123.333 26.628 74.98 74.98C26.629 123.333 0 187.62 0 256s26.629 132.668 74.98 181.02C123.333 485.372 187.62 512 256 512s132.667-26.628 181.019-74.98C485.372 388.667 512 324.38 512 256s-26.628-132.667-74.98-181.019zM256 482C131.383 482 30 380.617 30 256S131.383 30 256 30s226 101.383 226 226-101.383 226-226 226z" fill="#feca57"/>
                <path d="M371.793 290.457c-7.592-3.319-16.434.147-19.751 7.739-16.803 38.456-54.771 63.304-96.728 63.304-58.173 0-105.5-47.327-105.5-105.5s47.327-105.5 105.5-105.5c41.715 0 79.595 24.649 96.502 62.796 3.357 7.574 12.217 10.995 19.791 7.636 7.574-3.356 10.993-12.217 7.636-19.791-21.711-48.988-70.356-80.641-123.928-80.641-74.715 0-135.5 60.785-135.5 135.5s60.785 135.5 135.5 135.5c53.881 0 102.64-31.909 124.218-81.292 3.317-7.591-.148-16.434-7.74-19.751z" fill="#feca57"/>
                </svg>
                <span> {{currentYear}} Made with </span>
                <svg viewBox="0 -28 512 512" width="12" height="12" xmlns="http://www.w3.org/2000/svg">
                <path d="M471.383 44.578C444.879 15.832 408.512 0 368.973 0c-29.555 0-56.621 9.344-80.45 27.77C276.5 37.07 265.605 48.45 256 61.73c-9.602-13.277-20.5-24.66-32.527-33.96C199.648 9.344 172.582 0 143.027 0c-39.539 0-75.91 15.832-102.414 44.578C14.426 72.988 0 111.801 0 153.871c0 43.3 16.137 82.938 50.781 124.742 30.992 37.395 75.535 75.356 127.117 119.313 17.614 15.012 37.579 32.027 58.309 50.152A30.023 30.023 0 00256 455.516c7.285 0 14.316-2.641 19.785-7.43 20.73-18.129 40.707-35.152 58.328-50.172 51.575-43.95 96.117-81.906 127.11-119.305C495.867 236.81 512 197.172 512 153.867c0-42.066-14.426-80.879-40.617-109.289zm0 0" fill="#feca57"/>
                </svg>
                <span v-if="false"> for Matisse</span>
                <span> in Montreal</span>
            </div>
        </footer>
    </div>

</template>
<script>
import numberButton from './NumberButton.vue'
import numberButtonHorizontal from './NumberButtonHorizontal.vue'
import numberButtonVertical from './NumberButtonVertical.vue'

export default {
  name: 'multiplication-main-container',
  components: {
    numberButton,
    numberButtonHorizontal,
    numberButtonVertical,
  },
  data() {
    return {
        firstRowArray: [],
        firstColumnArray: [],
        resultArray: [],
        number: 8,
        numberFromColumn: 0,
        numberFromRow: 0,
        multiplicationResult: 0,
        activeLearn: false,
        clickable: false,
        randomNumberColumn: undefined,
        randomNumberRow: undefined,
        hiddenResult: 0,
        resultNumber: 0,
        userInput: '',
        goodAnswerCount: 0,
        wrongAnswerCount: 0,
        countDown: 10,
        timerObj: {},
        timeOutObj: {},
        isCorrectInput: false,
        placeholderEdited: 'Enter result',
        goodAnswerRow: 0,
        confettiTimeOut: {},
        numClicks: 0,
    }
  },
 created() {
    this.makeFirstRow(this.number);
    this.makeInsideGrid(this.number);
 },
 computed: {
    addMargin() {
        return {
        '--margin-top': `${((this.number - 5) * 100) + 40}px`,
        }
    },
    currentYear() {
        const today = new Date();
        return today.getFullYear();
    },
 },
  methods: {
    checkResult() {
        if(Number(this.userInput) === this.hiddenResult) {
            this.reset();
            this.goodAnswerCount++;
            this.goodAnswerRow++;
            this.placeholderEdited = 'Correct!'
            if(this.goodAnswerRow === 5) {
                this.$confetti.start();
                this.confettiTimeOut = setTimeout(() => {
                    this.$confetti.stop();
                    this.clearOut();
                }, 5000);    
            }
        } else {
            this.isCorrectInput = false;
        }
        this.userInput = '';
    },
    countDownTimer() {
        this.countDown = this.countDown - 1;
        if (this.countDown <= 0)
        {
            clearInterval(this.timerObj);
            this.timerObj = null;
            return;
        }
    },
    reset() {
        clearTimeout(this.timeOutObj);
        clearInterval(this.timerObj);
        this.countDown = 10;
        this.numClicks = 0;
    },
    runAgain() {
        this.isInputDisabled = false;
    },
    runTest() {
        if(this.goodAnswerRow === 5) {
            clearTimeout(this.confettiTimeOut);
            this.$confetti.stop();
            this.reset();
            this.clearOut();
        }
        this.$refs.userInput.focus();
        this.clickable = false;
        if(this.countDown < 10 && !this.isCorrectInput && this.resultNumber === 0) {
            return
        } else {
                this.resultNumber = 0;
                this.randomNumberColumn = Math.floor(Math.random() * this.number) + 1;
                this.randomNumberRow = Math.floor(Math.random() * this.number) + 1;
                this.timerObj = setInterval(this.countDownTimer, 1000);
                console.log(this.hiddenResult);
                this.timeOutObj = setTimeout(() => {
                        this.resultNumber = this.hiddenResult;
                        this.wrongAnswerCount++;
                        this.isInputDisabled = true;
                }, 10000);
            }
    },
    clearOut() {
        this.reset();
        this.placeholderEdited = 'Enter result'
        this.resultNumber = 0;
        this.goodAnswerCount = 0;
        this.goodAnswerRow = 0;
        this.wrongAnswerCount = 0;
        this.numberFromColumn = 0;
        this.numberFromRow = 0;
    },
    activateLearnMode() {
        this.reset();
        this.clearOut();
    },
    makeFirstRow(unit) {
        this.firstRowArray = [];
        for (let i = 0; i <= unit; i++) {
            this.firstRowArray.push(i);
        }
        return this.firstRowArray
    },
    makeInsideGrid(unit) {
        this.resultArray = [];
        let tempArray = [];
        for (let i = 1; i <= unit; i++) {
            tempArray = [];
            for (let j = 1; j <= unit; j++) {
                tempArray.push(i * j);
            }
            this.resultArray.push(tempArray);
        }
        return this.resultArray
    },
    decrease() {
        if(this.number > 1) {
            this.number--;
            this.makeFirstRow(this.number);
            this.makeInsideGrid(this.number)
        }
    },
    increase() {
        if(this.number < 10) {
            this.number++;
            this.makeFirstRow(this.number);
            this.makeInsideGrid(this.number)
        }
    },
    findItemColumn(numberShown) {
        if(this.multiplicationResult !== 0) {
            this.multiplicationResult = 0;
            this.numberFromColumn = 0;
            this.numberFromRow = 0;
        }

        this.numberFromColumn = numberShown;

        if(this.numberFromRow > 0 && this.numberFromColumn > 0) {
            this.multiplicationResult = this.numberFromRow * this.numberFromColumn;
        }
    },
    findItemRow(rowIndex) {
        if(this.multiplicationResult !== 0) {
            this.multiplicationResult = 0;
            this.numberFromColumn = 0;
            this.numberFromRow = 0;
        }
        this.numberFromRow = rowIndex + 1;
        console.log(this.numberFromRow);
        if(this.numberFromRow > 0 && this.numberFromColumn > 0) {
            this.multiplicationResult = this.numberFromRow * this.numberFromColumn;
        }
    }
  }
}
</script>
<style lang="less">
.multiplication-main-container {
    width: 1200px;
    height: 90vh;
    margin: 0 auto;
    font-family: 'Merriweather Sans', sans-serif;
    font-size: 14px;
    .scrollContainer {
        overflow-y: scroll;
        height: 92vh;
        .options {
            display: inline-flex;
            width: 185px;
            margin: auto;
            align-items: center;
            justify-content: space-between;
            .option-learn {
                display: inline-flex;
                padding: 4px 8px;
                font-family: 'Merriweather Sans', sans-serif;
                font-size: 16px;
                cursor: pointer;
                text-align: center;
                text-decoration: none;
                outline: none;
                color: #fff;
                background-color: #48dbfb;
                border: none;
                border-radius: 5px;
                &.option-learn:hover {background-color:#0abde3}
                &.activateLearn {
                    background-color: #2e86de;
                }
            }
            .test {
                font-family: 'Merriweather Sans', sans-serif;
                display: inline-flex;
                padding: 4px 8px;
                font-size: 16px;
                cursor: pointer;
                text-align: center;
                text-decoration: none;
                outline: none;
                color: #fff;
                background-color: #48dbfb;
                border: none;
                border-radius: 5px;
                &.test:hover {background-color:#0abde3}
                &.activateTest {
                    background-color: #2e86de;
                }
            }
            .change-table-size {
                display: inline-flex;
                justify-content: center;
                position: relative;
                .arrow {
                    align-items: center;
                }
                .input-width {
                    margin: 0 10px 0 10px;
                }
            }
        }
        .main-instruction {
            font-family: 'Merriweather Sans', sans-serif;
            .instruction {
                font-size: 16px;
                margin-top: 25px;
            }
            .result-score {
                position: relative;
                .multiplying-numbers {
                    position: relative;
                }
                .user-input {
                    align-items: center;
                    justify-content: center;
                    display: inline-flex;
                    align-items: center;
                    .input-side {
                        display: flex;
                        align-items: center;
                        justify-content: space-between;
                        width: 245px;
                        .result-input {
                        width: 100px;
                        height: 24px;
                        }
                        .correctInput {
                            background-color: greenyellow;
                        }
                        .enter {
                            font-family: 'Merriweather Sans', sans-serif;
                            font-size: 12px;
                            background-color: #2e86de;
                        }
                        .countdown {
                            width: 40px;
                            font-size: 16px;
                            font-weight: 600;
                        }
                        .run-test {
                            display: inline-block;
                            padding: 4px 8px;
                            font-family: 'Merriweather Sans', sans-serif;
                            font-weight: 700;
                            font-size: 14px;
                            cursor: pointer;
                            text-align: center;
                            text-decoration: none;
                            outline: none;
                            color: #fff;
                            background-color: #a4b5c5;
                            border: none;
                            border-radius: 15px;
                            box-shadow: 0 5px rgb(223, 222, 222);
                            &.isClickable {
                                background-color: #1dd1a1;
                                box-shadow: 0 5px rgb(180, 180, 180);
                                &.isClickable:hover {background-color:#10ac84}
                            }
                        }
                    }
                }
                .score {
                    display: inline-block;
                    margin-left: 50px;
                    span {
                        display: block;
                    }
                    .show-scores {
                        font-size: 18px;
                        display: inline-flex;
                        position: relative;
                        width: 100px;
                        height: 30px;
                        justify-content: space-evenly;
                        align-items: center;
                        .good-answer {
                            background-color: greenyellow;
                            width: 30px;
                            border-radius: 5px;
                        }
                        .wrong-answer {
                            background-color: #ff6464;
                            width: 30px;
                            border-radius: 5px;
                        }
                    }
                }
            }
        }
        .main-page {
            display: flex;
            margin: 15px auto;
            padding: 10px 0px 10px 5px;
            justify-content: center;
            .first-column {
                height: fit-content;
                display: inline-block;
                position: relative;
                top: 0;
                left: 0;
            }
            .center-panel {
                height: auto;
                display: inline-block;
                position: relative;
                .first-row {
                    width: fit-content;
                    display: block;
                    position: relative;
                    top: 0;
                    .first-row-item {
                        display: inline-block;
                        .number-button-row{
                            background-color: bisque;
                        }
                    }
                }
                .table {
                    display: block;
                    position: relative;
                    right: 0;
                    bottom: 0;
                    .single-row {
                        display: flex;
                        justify-content: center;
                    }
                }
            }
        }
    }
    
    .footer {
        position: relative;
        svg path:nth-last-of-type(1){
            color: #feca57;
        }
        span {
            color: #feca57;
        }
    }
}
</style>
