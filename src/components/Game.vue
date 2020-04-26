<template>
  <div id="game">
    <div id="life" class="grid-content" :style="getRange">
      <div
        class="cursor-pointer border-solid"
        :class="{'bg-black':value}"
        v-for="(value,index) in grid"
        :key="value.id"
        @click="changeValue(index)"
      >
      </div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";

export default {
  props: ["range","play"],
  data() {
    return {
      grid: this.makeGrid()
    };
  },
  computed: {
    getRange() {
      return {
        "--grid-columns": `repeat(${this.range.x},25px)`,
        "--grid-rows": `repeat(${this.range.y},25px)`
      };
    }
  },
  methods: {
    makeGrid() {
      const grid = [];
      for (let i = 0; i < this.range.x * this.range.y; i++) {
        grid.push(false);
      }
      console.log(grid);
      return grid;
    },
    changeValue(index) {
      const value = this.grid[index];
      Vue.set(this.grid, index, !value);
    },
    age() {
        const min = 0
        const max = this.range.x * this.range.y -1
        const y = this.range.y
        const x = this.range.x
        const newMatrix = []
        for(let i=0;i<y;i++){
            for(let j=0;j<x;j++){
                let dot = i*x + j
                let number = 0

                for(let k=-1;k<=1;k++){
                    for(let l=-1;l<=1;l++){
                        let current = (i+k) * x + (j+l)
                        if(min <= current <= max  && i+k >=0 && j+l >=0){
                            if(this.grid[current]){
                            number+=1
                        }
                        }
                    }
                }
                newMatrix[dot] = false

                if(this.grid[dot]){
                    if(number>2 && number <=4){newMatrix[dot] = true}
                }
                else{
                    if(number == 3){newMatrix[dot] = true}
                }
                
            }
        }
            for(let i=0;i<=max;i++){
                Vue.set(this.grid,i,newMatrix[i])
            }
    }
      
  },
  mounted(){
      setInterval(() => {
          if(this.play){
              this.age()
          }
      },200)
  }
};
</script>

<style>
.grid-content {
  display: grid;
  grid-template-columns: var(--grid-columns);
  grid-template-rows: var(--grid-rows);
  justify-content: center;
  align-content: center;
}

.border-solid {
  border-style: solid;
  border-width: 1px;
  border-color: #cacaca;
}

.cursor-pointer {
  cursor: pointer;
}

.bg-black {
    border-color: black;
  background-color: black;
}

#game {
  display: grid;
  grid-template-rows: 100px 1fr 100px;
  grid-template-columns: 400px 1fr 400px;
  grid-template-areas:
    "nothing menu nothing3"
    "life life life"
    "nothing2 nothing2 nothing2";
  height: 100vh;
}

#life {
  grid-area: life;
}
</style>