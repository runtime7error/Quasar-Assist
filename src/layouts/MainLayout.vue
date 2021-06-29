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

    <!-- Dialog de ficha criada -->
    <div style="position: relative; top: 100px">
      <q-page-container class="row justify-start content-end" v-if="fichaState">
        <div
          class="q-ma-lg"
          style="margin-right: 30px"
          :key="ficha.id"
          v-for="ficha in containerFicha"
          @click="exibirFicha(ficha)"
        >
          <q-card class="dialog-border null-card">
            <q-input
              :label="ficha.name"
              class="q-ma-lg"
              dense
              rounded
              outlined
              color="purple-4"
              bg-color="white"
              readonly
            />
            <!-- <q-input
              clearable
              clear-icon="close"
              filled
              color="purple-12"
              v-model="ficha.name"
              label="Label"
            /> -->
            <q-input
              class="q-ma-lg"
              dense
              rounded
              outlined
              color="purple-4"
              bg-color="white"
              readonly
              :label="ficha.age.toString()"
            />
            <q-input
              :label="ficha.breed"
              class="q-ma-lg"
              dense
              rounded
              outlined
              color="purple-4"
              bg-color="white"
              readonly
            />
          </q-card>
        </div>
      </q-page-container>
    </div>

    <!-- Dialogo de Exibição -->
    <q-page-container>
      <q-dialog v-model="fichaDialog">
        <div
          :key="ficha.id"
          v-for="ficha in containerFicha"
          class="q-pa-md null-card dialog-border"
          style="max-width: 400px"
        >
          <q-input
            clearable
            v-model="ficha.name"
            class="q-ma-lg"
            dense
            rounded
            outlined
            color="purple-4"
            bg-color="white"
          />
          <q-input
            clearable
            v-model="ficha.age"
            class="q-ma-lg"
            dense
            rounded
            outlined
            color="purple-4"
            bg-color="white"
          />
          <q-input
            clearable
            v-model="ficha.breed"
            class="q-ma-lg"
            dense
            rounded
            outlined
            color="purple-4"
            bg-color="white"
          />
          <q-btn
            class="q-ma-lg"
            color="red"
            label="Excluir"
            rounded
            @click="removeFicha(ficha.id)"
          />
          <q-btn
            color="green"
            label="Salvar"
            rounded
            type="submit"
            class="q-ml-xl"
            @click="onSave"
          />
        </div>
      </q-dialog>
    </q-page-container>

    <!-- Dialog de criação -->
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
                @click="onSave"
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

let db = new Localbase("db");

export default {
  data() {
    return {
      text: "",
      data: "teste",
      name: "",
      age: "",
      breed: "",
      fichaState: false,
      prompt: false,
      userData: [],
      containerFicha: [],
      fichaDialog: false,
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
      db.collection("fichas").add(Ficha);
      this.containerFicha.push(Ficha);
      this.saveFicha();
    },

    onClose() {
      this.prompt = false;
    },
    saveFicha() {
      console.log(this.userData);
      this.prompt = false;
      this.fichaState = true;
    },
    removeFicha(id) {
      db.collection("fichas").doc({ id: id }).delete();
      console.log("id", id);
      this.getFicha();
    },
    exibirFicha() {
      console.log("exibindo ficha :D");
      this.fichaDialog = true;
    },
    getFicha() {
      db.collection("fichas")
        .get()
        .then((resp) => {
          this.userData = resp;
          this.containerFicha = resp;
          console.log("ficha inicial", this.userData);
          this.prompt = false;
        });
    },
    editSave() {
      let index = this.userData.find((resp) => Ficha.id === id);
      db.collection("ficha").doc({ id: id }).update({});
    },
  },
  mounted() {
    this.getFicha();
    if (this.userData.length > 0) {
      this.fichaState = !this.fichaState;
    }
  },
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
      rgba(150, 59, 240, 0.672),
      rgba(137, 88, 217, 0.8)
    ),
    #ffffff;
}

.null-card {
  background: linear-gradient(151.23deg, rgba(175, 92, 215, 0.71), #9150e4);
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