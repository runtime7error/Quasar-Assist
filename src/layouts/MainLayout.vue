<template>

  <!-- navbar -->
  <q-layout view="lHh Lpr LFf" class="header">
    <q-header elevation="0">
      <q-toolbar class="header">
        <div>
          <q-toolbar-title class="text-h6"
            ><strong>RPG</strong>Assist</q-toolbar-title
          >
        </div>
        <q-space></q-space>
        <div class="gt-xs">
          <q-btn rounded flat label="Home" class="q-ml-xs" />
          <q-btn rounded flat label="Criar" class="q-ml-xs" @click="create" />
          <q-btn rounded flat label="Fichas" class="q-ml-xs" />
        </div>
        <div class="gt-xs">
          <q-input
            dense
            rounded
            outlined
            v-model="text"
            color="purple-4"
            bg-color="white"
            placeholder="Digite sua busca"
          >
            <template v-slot:append>
              <q-icon v-if="text === ''" name="search" />
              <q-icon v-else name="clear" @click="text = ''" />
            </template>
          </q-input>
        </div>
        <div class="lt-sm">
          <q-btn flat dense round icon="menu" aria-label="menu"> </q-btn>
        </div>
      </q-toolbar>
    </q-header>


    <!-- Tela sem ficha -->
    <q-page-container v-if="!fichaState" class="row text-h6">
      <div class="fixed-center" style="min-width: 200px">
        <q-card bordered dark class="null-card dialog-border">
          <q-card-section class="row justify-center"
            >Parece que você não possui fichas cadastradas, clique no botão para
            criar uma agora mesmo !
            <q-btn
              rounded
              flat
              label="Criar"
              size="lg"
              style="margin-right: 5px"
              @click="create"
            />
          </q-card-section>
        </q-card>
      </div>
    </q-page-container>


    <!-- Dialog da ficha -->
    <q-page-container class="row justify-start content-end" v-if="fichaState">
      <div style="position: relative; top: 100px; margin-left: 30px">
        <q-card class="dialog-border null-card q-gutter-md">
          <q-input dense rounded outlined color="purple-4" bg-color="white"
          placeholder: this.userData.name readonly />
          <q-btn color="red" label="Excluir" rounded @click="removeFicha" />
        </q-card>
      </div>
    </q-page-container>

    <q-page-container>
      <q-dialog v-model="prompt" persistent>
        <div class="q-pa-md null-card dialog-border" style="max-width: 400px">
          <q-form @submit="onSave" @reset="onClose" class="q-gutter-md">
            <q-card-section>
              <div class="text-h6 q-gutter-md">Criação de Ficha</div>
            </q-card-section>

            <q-input
              dense
              rounded
              outlined
              color="purple-4"
              bg-color="white"
              placeholder="Nome"
              lazy-rules
              v-model="name"
              :rules="[
                (val) =>
                  (val && val.length > 0) || 'Nome não pode ficar vazio !',
              ]"
            />

            <q-input
              dense
              rounded
              outlined
              color="purple-4"
              bg-color="white"
              placeholder="Idade"
              mask="#########"
              lazy-rules
              v-model="age"
              :rules="[
                (val) =>
                  (val !== null && val !== '') || 'Por favor digite a idade',
              ]"
            />

            <q-input
              dense
              rounded
              outlined
              color="purple-4"
              bg-color="white"
              placeholder="Raça"
              lazy-rules
              v-model="breed"
              :rules="[
                (val) =>
                  (val && val.length > 0) || 'Raça não pode ficar vazio !',
              ]"
            />

            <div>
              <q-btn color="red" label="Cancelar" rounded type="reset" />
              <q-btn
                color="green"
                label="Salvar"
                rounded
                type="submit"
                class="q-ml-xl"
              />
            </div>
          </q-form>
        </div>
      </q-dialog>
    </q-page-container>
  </q-layout>
</template>

<script src="https://unpkg.com/localbase/dist/localbase.dev.js"></script>

<script>
import EssentialLink from "components/EssentialLink.vue";
import Localbase from "localbase";

export default {
  data() {
    let db = new Localbase("db");
    return {
      text: "",
      name: "",
      age: "",
      breed: "",
      fichaState: false,
      prompt: false,
      userData: [{}],
    };
  },
  methods: {
    create() {
      this.prompt = true;
    },
    onSave() {
      if (!this.userData) {
        return;
      }
      let Ficha = {
        id: Math.random(),
        name: this.name,
        age: this.age,
        breed: this.breed,
      };
      this.userData.push(Ficha);
      this.saveFicha();
      this.Ficha = "";
    },
    onClose() {
      this.prompt = false;
      this.fichaState = false;
    },
    saveFicha() {
      console.log(this.userData);
      this.prompt = false;
      this.fichaState = true;
    },
    removeFicha(id) {
      let index = this.Ficha.findIndex((Ficha) => Ficha.id === id);
      this.Ficha.splice(index, 1);
    },
  },
  watch: {},
};
</script>
<style lang="scss">
@font-face {
  font-family: Montserrat;
  src: url("../fonts/montserrat-v15-latin-regular.woff") format("woff");
}

div {
  color: #ffffff;
}

.header {
  font-family: "Montserrat";
  background: linear-gradient(
      125deg,
      rgba(150, 59, 240, 0.672) 36.89%,
      rgba(137, 88, 217, 0.8) 84.8%
    ),
    #ffffff;
}

.null-card {
  background: linear-gradient(
    151.23deg,
    rgba(175, 92, 215, 0.71) 27.68%,
    #9150e4 71.7%
  );
  box-shadow: 5px 5px 12px -1px rgba(0, 0, 0, 0.25);
  border-radius: 8px;
  font-family: "Montserrat";
}

.q-field--outlined:hover .q-field__control:before {
  border-color: #ba68c8;
}

.dialog-border {
  border-color: blanchedalmond;
  border-style: groove;
  border-width: 1pt;
  border-radius: 8pt;
}
</style>