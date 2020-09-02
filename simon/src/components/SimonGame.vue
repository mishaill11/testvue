<template>
  <div class="wrapper">
    <h1>Simon Says</h1>
    <div class="game_zone">
      <div class="game_zone__field">
        <div 
          class="field_color"
          ref="field_color"
          v-for="color in colors"
          :key="color"
          :style="{background: color}"
        >
        </div> 
      </div>
      <div class="game_zone__control">
        <h2>Раунд {{ round }}</h2>
        <p v-if="lose">Ты проиграл</p>
        <button @click.prevent="startGame" class="control_btn">Старт</button>
        <p>Уровни сложности:</p>
        <div 
          v-for="lvl in levels"
          :key="lvl.lvl"
        >
          <p>{{ lvl.lvl }}</p>
          <input ref="levels" type="radio" :value="lvl.levelSpeed" class="levels">
        </div>
      </div>
      
    </div>
  </div>
</template>

<script>
export default {
  name: 'SimonGame',
  data() {
    return {
      arrComp: [],
      round: 1,
      lose: false,
      colors: {
        c1: '#4169E1',
        c2: '#DC143C',
        c3: '#FFD700',
        c4: '#228B22'
      },
      levels: {
        l1: {
          lvl: 'Первый',
          levelSpeed: 1500,
          check: 'checked'
        },
        l2: {
          lvl: 'Второй',
          levelSpeed: 1000
        },
        l3: {
          lvl: 'Третий',
          levelSpeed: 400
        },
      },
      sound: {
        do: {
          id: 0,
          name: 'noty-do.mp3'
        },
        re: {
          id: 1,
          name: 're.mp3'
        },
        mi: {
          id: 2,
          name: 'mi.mp3'
        },
        fa: {
          id: 3,
          name: 'fa.mp3'
        }
      },
      levelSpeed: 1500,
      s: 0
    }
  },
  methods: {
    getSound(i) {
      for (let snd in this.sound) {
        if (i === this.sound[snd].id) {
          let audio = new Audio(require(`../sound/${this.sound[snd].name}`))
          audio.play()
        }
      }
    },
    getRandomIntInclusive(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
    startAlg() {
      let square = document.querySelectorAll('.field_color')

      square.forEach(elem => {
        elem.classList.remove('disabled')
      })
      
      let roundTime = setInterval(() => {
        let rand = this.getRandomIntInclusive(0, square.length - 1)
        this.getSound(rand)
        square[rand].style.opacity = 1
        setTimeout(() => square[rand].style.opacity = .5, 200)
        this.arrComp.push(rand)
      }, this.levelSpeed)
      setTimeout(() => {clearInterval(roundTime);}, this.levelSpeed * this.round)
    },
    startGame() {
      this.lose = false
      this.startAlg()
      let square = this.$refs.field_color
      this.s = 0

      square.forEach((elem, i) => elem.addEventListener('click', () => {
        this.getSound(i)
        setTimeout(() => elem.style.opacity = .5, 200)
          if (this.arrComp[this.s] === i) {
            elem.style.opacity = 1
            this.s++
          } else {
            square.forEach(elem => {
              elem.classList.add('disabled')
            })
            this.lose = true
            setTimeout(() => location.reload(), 1500)
          } 
          if (this.arrComp.length === this.s) {
            this.round++
            this.startAlg() 
          }
        }
      )) 
    }
  },
  mounted() {
    let levels = this.$refs.levels
    levels[0].checked = true

    levels.forEach(elem => elem.addEventListener('click', () => {
      levels.forEach(elem => elem.checked = false)
      elem.checked = true
      this.levelSpeed = elem.value
    }))
     
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
  .wrapper {
    display: flex;
    flex-direction: column;
    // justify-content: center;
    align-items: center;
  }
  .game_zone {
    display: flex;
    width: 50%;
    justify-content: space-around;  
  }

  .game_zone__field {
      display: flex;
      flex-wrap: wrap;
      margin: 0 auto;
      width: 400px;
      margin: 0;    
  }
  
  .field_color {
    width: 200px;
    height: 200px;
    opacity: .5;
  }

  .control_btn {
    width: 100px;
    height: 50px;
    font-size: 25px;
    color: aliceblue;
    background-color: #DC143C;
    border-radius: 20px;
  }

  .disabled {
    pointer-events: none;
  }
</style>
