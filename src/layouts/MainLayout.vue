<template>
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
          <q-btn rounded flat label="Criar" class="q-ml-xs" @click="create()" />
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
    <q-drawer> </q-drawer>
    <q-page-container v-if="!ficha" class="row text-h6 ">
      <div class="fixed-center" style="min-width: 200px">
        <q-card bordered dark class="null-card dialog-border">
          <q-card-section class="row justify-center"
            >Parece que você não possui fichas cadastradas, clique no botão
            para criar uma agora mesmo !
            <q-btn
              rounded
              flat
              label="Criar"
              size="lg"
              style="margin-right: 5px"
              @click="create()"
            />
          </q-card-section>
        </q-card>
      </div>
    </q-page-container>

    <q-page-container v-if="ficha">
      <q-dialog v-model="prompt" persistent>
        <div v-if="dialog" class="q-pa-md null-card dialog-border" style="max-width: 400px">
          <q-form class="q-gutter-md">
            <q-card-section>
              <div class="text-h6 q-gutter-md " >Criação de Ficha</div>
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
              <q-btn
                color="red"
                label="Cancelar"
                rounded
                @click="onClose()"
              />
              <q-btn
                color="green"
                label="Salvar"
                rounded
                @click="onSave()"
                class="q-ml-xl"
              />
            </div>
          </q-form>
        </div>
      </q-dialog>
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from "components/EssentialLink.vue";

export default {
  data() {
    return {
      text: "",
      ficha: false,
      prompt: false,
      name: "",
      age: "",
      breed: "",
      dialog: false,
    };
  },
  methods: {
    create() {
      console.log("Ficha Criada !!!");
      this.ficha = true;
      this.prompt = true;
      this.dialog = true;
    },
    onSave() {
      this.dialog = false;
      this.ficha = false;
    },
    onClose() {
      this.dialog = false;
      this.ficha = false;
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

div{
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

.dialog-border{
  border-color: blanchedalmond;
  border-style: groove;
  border-width: 1pt;
  border-radius: 8pt;

}
</style>