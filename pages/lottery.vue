<template>
  <div class="container">
    <h1>
      Lottary
    </h1>
    <div class="col">
      <b-button variant="success" v-on:click="handleData()" size="sm" class="mt-4"
                style="float:right;text-align:right">submit
      </b-button>
    </div>
    <div class="row d-flex justify-content-center mt-5 col-12" style="height: 100%">
      <div v-for="array in arrays" class="col-3 row d-flex justify-content-center p-0 mt-1">
        <div v-for="value in array" class="col-1 box-style-2" align="center">
          <span style="font-size: 20px">
            {{value}}
          </span>
        </div>
      </div>
    </div>
    <div class="col-12 row justify-content-center mt-3" v-if="arrayObj != ''">
      <h1>เลขท้าย3ตัว</h1>
      <b-table striped hover :items="arrayObj"></b-table>
    </div>
  </div>
</template>

<script>
  export default {
    name: "lottery",
    data: () => ({
      player: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
      dog: `test`,
      row: 20,
      col: 6,
      arrays: [],
      arrayObj: []
    }),
    mounted() {
      this.handleData()
    },
    methods: {
      careateDimension() {
        const {player, row, col} = this
        let dimensions = []
        let array = player
        for (let i = 0; i < row; i++) {
          dimensions.push([])
          for (let j = 0; j < col; j++) {
            dimensions[i][j] = array[Math.floor(Math.random() * array.length)]
          }
        }
        this.arrays = dimensions
      },
      handleSliceArray() {
        const {arrays} = this
        let resp = []
        let uniqueKey = null
        let obj = []
        for (let i = 0; i < arrays.length; i++) {
          resp.push(arrays[i].slice(3).toString().replace(/,/g, ''))
        }
        uniqueKey = Array.from(new Set(resp))
        for (let i = 0; i < uniqueKey.length; i++) {
          let result = resp.filter(resp => resp === uniqueKey[i]);
          let res = result.length
          obj.push({number: uniqueKey[i], count: result.length})
        }
        return obj
      },
      setObjToState(obj) {
        let array = []
        obj.forEach(element => {
            if (element.count > 1) {
              array.push(element)
            }
          }
        )
        return array
      },
      async handleData() {
        await this.careateDimension()
        let obj = await this.handleSliceArray()
        let res = await this.setObjToState(obj)
        this.arrayObj = res
      }

    },
  }
</script>

<style scoped>
  .box-style-2 {
    /*border-radius: 15px;*/
    background: #ffffff;
    box-shadow: 2px 2px 6px #dedede,
    -5px -5px 17px #ffffff;
  }

  .container {
    margin: 0 auto;
    min-height: 50vh;
    /*display: flex;*/
    justify-content: center;
    align-items: center;
    text-align: center;
  }
</style>
