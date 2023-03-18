<template>
  <div>
    <div class="center">
      <h1>POKEDEX</h1>
    </div>

    <div class="flex">
      <div class="flex-col">

        <div v-for="(p, index) in pokemons" :key="index" @click="SendInfo(p)">
          <v-card 
            class="mx-auto"
            max-width="344"
            outlined
          >
          <v-list-item three-line>
            <v-list-item-content>
              <div class="text-overline mb-4">
                Tipo
              </div>
              <v-list-item-title class="text-h5 mb-1">
                {{p.name}} 
              </v-list-item-title>
              <v-list-item-subtitle>Descripcion breve del pokemon</v-list-item-subtitle>
            </v-list-item-content>
            <v-img
              :src="p.img"
              max-height="140px"
              max-width="140px"
            ></v-img>
          </v-list-item>
          </v-card>
        </div>

      </div>
      <div class="flex-col">    
        <PokeInfo
          :pokemon-info="selected_pokemon"
        />
        
      </div>
    </div>
    



  </div>
</template>

<script>
  import axios from 'axios'
  import PokeInfo from '../components/PokeInfo.vue'

  export default {
    name: 'Home',
    components: {
      PokeInfo
    },
    data(){
      return{
        pokemons: [],
        selected_pokemon: []
        
      }
    },
    created(){
      for(let i = 0; i <= 10; i++){
        axios.get(`https://pokeapi.co/api/v2/pokemon/${i + 1}`)
        .then(res => {
          // console.log(res.data)
          let pokemon =  {
            img: res.data.sprites.front_default,
            name: res.data.name ,
            abilility: res.data.abilities
        }
        this.pokemons.push(pokemon)
        })
      }
    },
    methods:{
      SendInfo(data){
        this.selected_pokemon = data
      }
    }
  }
</script>

<style scoped>
.center {
  text-align: center;
  margin-top: 10px;
}
.flex{
  display: flex;
}

.flex-col{
  flex: 1;
  background-color: aquamarine;
  
}
</style>
