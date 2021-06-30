<template>
  <div>
    <q-header elevation="0">
      <q-toolbar class="header">
        <div>
          <q-toolbar-title class="text-h6">
            <strong>RPG</strong>Assist
          </q-toolbar-title>
        </div>
        <q-space></q-space>
        <div class="gt-xs">
          <q-btn rounded flat label="Home" class="q-mr-xs" />
          <q-btn
            rounded
            flat
            label="Criar"
            class="q-ml-xs"
            @click="handleClick"
          />
          <q-btn rounded flat label="Fichas" class="q-mr-xs" />
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
          <q-btn @click="drawer = !drawer" flat dense round icon="menu" aria-label="menu"> </q-btn>
        </div>
      </q-toolbar>
    </q-header>
    <q-drawer
      class="lt-sm"
      v-model="drawer"
      side="right"
      :width="200"
      :breakpoint="100"
      overlay
      elevated
      content-class="header"
      behavior="mobile"
      bordered
    >
      <q-list>
        <q-item>
          <q-item-section>
            <q-btn 
            flat
            label="Home" 
            rounded 
            />
          </q-item-section>
        </q-item>
        <q-separator inset color="purple"/>
        <q-item>
          <q-item-section>
            <q-btn
              rounded
              flat
              label="Criar"
              @click="handleClick"
            />
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>
  </div>
</template>

<script>
export default {
  emits: ['createRecord'],
  data: () => ({
    text: '',
    drawer: false,
  }),
  methods: {
    handleClick() {
      this.$emit('createRecord')
    },
  },
}
</script>

<style>
</style>
