<template>
  <div class="q-pa-md null-card dialog-border" style="max-width: 400px">
    <q-form @submit="handleSave" @reset="handleClose" class="q-gutter-md">
      <q-card-section>
        <div class="text-h6 q-gutter-md">Criação de Ficha</div>
      </q-card-section>
      <!-- Nome -->
      <q-input
        dense
        rounded
        outlined
        color="purple-4"
        bg-color="white"
        placeholder="Nome"
        lazy-rules
        v-model="record.name"
        :rules="[
          value => (value && value.length > 0) || 'Nome não pode ficar vazio!',
        ]"
        required
      />
      <!-- Idade -->
      <q-input
        dense
        rounded
        outlined
        color="purple-4"
        bg-color="white"
        placeholder="Idade"
        mask="#########"
        lazy-rules
        v-model="record.age"
        :rules="[
          value => (value !== '' && +value > 0) || 'Por favor digite a idade',
        ]"
        required
      />
      <!-- Raça -->
      <q-input
        dense
        rounded
        outlined
        color="purple-4"
        bg-color="white"
        placeholder="Raça"
        lazy-rules
        v-model="record.breed"
        :rules="[
          value => (value && value.length > 0) || 'Raça não pode ficar vazio !',
        ]"
        required
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
</template>

<script>
export default {
  emits: ['create', 'close'],
  data: () => ({
    display: true,
    record: {
      name: '',
      age: '',
      breed: '',
    },
  }),
  methods: {
    handleSave() {
      this.$emit('create', this.record)
    },
    handleClose() {
      this.$emit('close')
    },
  },
}
</script>

<style>
</style>
