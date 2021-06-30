<template>
  <q-header elevation="0">
    <q-toolbar class="header">
      <div>
        <q-toolbar-title class="text-h6">
          <strong>RPG</strong>Assist
        </q-toolbar-title>
      </div>
      <q-space></q-space>
      <div class="gt-xs">
        <q-btn rounded flat label="Home" class="q-ml-xs" />
        <q-btn
          rounded
          flat
          label="Criar"
          class="q-ml-xs"
          @click="handleClick"
        />
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
</template>

<script>
export default {
  emits: ['createRecord'],
  data: () => ({
    text: '',
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
