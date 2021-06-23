<template>
  <q-layout view="lHh Lpr LFf" class="header">
    <q-header elevation="0">
      <q-toolbar class="header">
        <div>
          <q-toolbar-title class="text-h6"><strong>RPG</strong>Assist</q-toolbar-title>
        </div>
        <q-space></q-space>
        <div class="gt-xs">
          <q-btn rounded flat label="Home" class="q-ml-xs"/>
          <q-btn rounded flat label="Criar" class="q-ml-xs" @click="create()"/>
          <q-btn rounded flat label="Fichas" class="q-ml-xs"/>
        </div>  
        <div class="gt-xs">
          <q-input dense rounded outlined v-model="text" color="purple-4" bg-color="white" placeholder="Digite sua busca">
            <template v-slot:append>
              <q-icon v-if="text === ''" name="search" /> 
              <q-icon v-else name="clear" @click="text = ''" />
            </template>
          </q-input>
        </div>
        <div class="lt-sm">
          <q-btn
            flat
            dense
            round
            icon="menu"
            aria-label="menu"
            > 
          </q-btn>
        </div>
      </q-toolbar>
    </q-header>
   <q-drawer
   >

   </q-drawer>
    <q-page-container v-if="!ficha" class="row text-h5 justify-center">
      <div class="fixed-center" style="min-width: 200px">
        <q-card bordered dark class="null-card">
          <q-card-section>Parece que você não possui fichas cadastradas :( 
            <br/>Clique no botão para criar uma agora mesmo !
            <q-btn dense rounded flat label="Criar" size="lg" style="margin-right:5px" @click="create()"/>
          </q-card-section>
        </q-card>
      </div>
    </q-page-container>

    <q-page-container v-if="ficha" class="row text-h5 justify-center">
      <div class="fixed-center">
        <q-card bordered dark class="null-card">
          <q-card-section>
            Criação de ficha
            </q-card-section>
        </q-card>
      </div>
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from 'components/EssentialLink.vue'

export default {
  data () {
    return {
      text: "",
      ficha: false,
     
      
    }
  },
  methods:{
    create(){
      console.log("Ficha Criada !!!");
      this.ficha = true;
    },
    
  },
  watch: {
    
  }
}
</script>
<style lang="scss" scoped>

@font-face {
  font-family: Montserrat;
  src: url('../fonts/montserrat-v15-latin-regular.woff') format('woff');
}

.header {
  font-family: 'Montserrat';
  background: linear-gradient(125deg, rgba(150, 59, 240, 0.672) 36.89%, rgba(137, 88, 217, 0.8) 84.8%), #FFFFFF;

}

.null-card{
  background: linear-gradient(151.23deg, rgba(175, 92, 215, 0.71) 27.68%, #9150E4 71.7%);
  box-shadow: 5px 5px 12px -1px rgba(0, 0, 0, 0.25);
  border-radius: 8px;
  
  
}


</style>