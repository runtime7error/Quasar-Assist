<template>
  <div class="q-pa-md null-card dialog-border" style="max-width: 400px">
    <q-input
      clearable
      v-model="editRecord.name"
      class="q-ma-lg"
      dense
      rounded
      outlined
      color="purple-4"
      bg-color="white"
    />
    <q-input
      clearable
      v-model="editRecord.age"
      class="q-ma-lg"
      dense
      rounded
      outlined
      color="purple-4"
      bg-color="white"
    />
    <q-input
      clearable
      v-model="editRecord.breed"
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
      @click="handleDeleteRecord(record.id)"
    />
    <q-btn
      color="green"
      label="Salvar"
      rounded
      type="submit"
      class="q-ml-xl"
      @click="handleEditRecord(record.id)"
    />
  </div>
</template>

<script>
export default {
  props: ['record'],
  emits: ['editRecord', 'deleteRecord'],
  data: () => ({
    editRecord: {},
  }),
  methods: {
    handleEditRecord(id) {
      this.$emit('editRecord', {
        id,
        record: this.editRecord,
      })
    },
    handleDeleteRecord(id) {
      this.$emit('deleteRecord', {
        id,
      })
    },
  },
  // Gambiarra por conta do ciclo de vida do Vue
  beforeMount() {
    const { id, breed, name, age } = this.record
    this.editRecord = {
      id,
      breed,
      name,
      age,
    }
  },
}
</script>

<style>
</style>
