<template>
  <div class="container">
    <div class="col-12">
      <div class="row d-flex">
        <div class="col-2">
          <span>Player</span>
          <b-form-input v-model="player" placeholder="player" size="sm"></b-form-input>
        </div>
        <div class="col-2">
          <span>Row</span>
          <b-form-input v-model="row" placeholder="row" size="sm"></b-form-input>
        </div>
        <div class="col-2">
          <span>Column</span>
          <b-form-input v-model="col" placeholder="column" size="sm"></b-form-input>
        </div>
        <div class="col">
          <b-button variant="success" v-on:click="handleFuncLine()" size="sm" class="mt-4"
                    style="float:right;text-align:right">submit
          </b-button>
        </div>
      </div>
      <div col-12 class="row d-flex justify-content-center mt-5" style="height: 100%">
        <div v-for="array in arrays" class="col-8 row d-flex justify-content-center">
          <div v-for="value in array" class="col-1 box-style-2" align="center">
          <span style="font-size: 40px">
            {{value}}
          </span>
          </div>
        </div>
      </div>
    </div>
    <div class="col-12 row justify-content-center mt-3" v-if="number != ''">
      <div class="col-8" v-for="value in number">
        <div v-for="(valueN,key) in value " v-if="valueN != ''">
          <h1>Result</h1>
          <b-table striped hover :items="valueN"></b-table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data: () => ({
      player: 'x,o',
      dog: `test`,
      row: 4,
      col: 4,
      arrays: [
        ['o', 'x', 'o', 'x'],
        ['x', 'o', 'o', 'o'],
        ['o', 'x', 'x', 'x'],
        ['x', 'o', 'x', 'o'],
      ],
      number: [],
      items: [
        {age: 40, first_name: 'Dickerson', last_name: 'Macdonald'},
        {age: 21, first_name: 'Larsen', last_name: 'Shaw'},
        {age: 89, first_name: 'Geneva', last_name: 'Wilson'},
        {age: 38, first_name: 'Jami', last_name: 'Carney'}
      ],
    }),
    mounted() {
      this.handleData()
    },
    methods: {
      handleData() {
        const {player, row, col} = this
        let dimensions = []
        let array = player.split(",")
        if(row === col ){
          for (let i = 0; i < row; i++) {
          dimensions.push([])
          for (let j = 0; j < col; j++) {
            dimensions[i][j] = array[Math.floor(Math.random() * array.length)]
          }
        }
        this.arrays = dimensions
        }else{
          alert("กรุณาใส่ row กับ column ให้เท่ากัน")
        }

      },
      async handleFuncLine() {
        await this.handleData()
        const {arrays, number} = this
        let res = []
        res.push(this.verticalLine(arrays))
        res.push(this.horizontalLine(arrays))
        res.push(this.crossLineLeft(arrays))
        res.push(this.crossLineRight(arrays))
        this.number = res
      },
      verticalLine(array) {
        let resArray = {verticalLine: []}
        let x = null
        let bool = false
        let idx = null
        array.forEach((eachArray, idxA) => {
          eachArray.forEach((eachValue, idxV) => {
            if (idxV === 0) {
              x = array[idxA][idxV]
              bool = true
            } else if (x === array[idxA][idxV] && bool) {
              x = array[idxA][idxV]
              idx = idxA + 1
              bool = true
            } else {
              x = array[idxA][idxV]
              bool = false
            }
          })
          if (bool) {
            resArray.verticalLine.push({player: [x, x, x, x], bool: bool, line: 'Row ' + idx})
          }
        })
        return resArray
      },
      horizontalLine(array) {
        let resArray = {horizontalLine: []}
        let x = null
        let bool = false
        let idx = null
        array.forEach((eachArray, idxA) => {
          eachArray.forEach((eachValue, idxV) => {
            if (idxV === 0) {
              x = array[idxV][idxA]
              bool = true
            } else if (x === array[idxV][idxA] && bool) {
              x = array[idxV][idxA]
              idx = idxA + 1
              bool = true
            } else {
              x = array[idxV][idxA]
              bool = false
            }
          })
          if (bool) {
            resArray.horizontalLine.push({player: [x, x, x, x], bool: bool, line: 'Column ' + idx})
          }
        })
        return resArray
      },
      crossLineLeft(array) {
        let resArray = {crossLine: []}
        let x = null
        let bool = false
        array.forEach((eachArray, idxA) => {
          eachArray.forEach((eachValue, idxV) => {

            if (idxV === 0) {
              x = array[idxV][idxV]
              bool = true
            } else if (x === array[idxV][idxV] && bool) {
              x = array[idxV][idxV]
              bool = true
            } else {
              x = array[idxV][idxV]
              bool = false
            }
          })
        })
        if (bool) {
          resArray.crossLine.push({player: [x, x, x, x], bool: bool, line: 'crossLineLeft'})
        }
        return resArray
      },
      crossLineRight(array) {
        let resArray = {crossLine: []}
        let x = null
        let bool = false
        array.forEach((eachArray, idxA) => {
          eachArray.forEach((eachValue, idxV) => {
            let lengthArray = (eachArray.length - 1)
            if (idxV === 0) {
              x = array[idxV][lengthArray - idxV]
              bool = true
            } else if (x === array[idxV][lengthArray - idxV] && bool) {
              x = array[idxV][lengthArray - idxV]
              bool = true
            } else {
              x = array[idxV][lengthArray - idxV]
              bool = false
            }
          })
        })
        if (bool) {
          resArray.crossLine.push({player: [x, x, x, x], bool: bool, line: 'crossLineRight'})
        }
        return resArray
      },
    },
  }
</script>

<style>
  .container {
    margin: 0 auto;
    min-height: 50vh;
    /*display: flex;*/
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  .title {
    font-family: 'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
    display: block;
    font-weight: 300;
    font-size: 100px;
    color: #35495e;
    letter-spacing: 1px;
  }

  .subtitle {
    font-weight: 300;
    font-size: 42px;
    color: #526488;
    word-spacing: 5px;
    padding-bottom: 15px;
  }

  .links {
    padding-top: 15px;
  }

  .box-style-2 {
    /*border-radius: 15px;*/
    background: #ffffff;
    box-shadow: 2px 2px 6px #dedede,
    -5px -5px 17px #ffffff;
  }
</style>
