<template>
  <div class="q-pa-md null-card dialog-border" style="max-width: 600px; width: 70%">
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
    <q-input
      clearable
      v-model="editRecord.gender"
      class="q-ma-lg"
      dense
      rounded
      outlined
      color="purple-4"
      bg-color="white"
    />
    <q-input
      clearable
      v-model="editRecord.kit"
      class="q-ma-lg"
      dense
      rounded
      outlined
      color="purple-4"
      bg-color="white"
    />
    <q-input
      clearable
      v-model="editRecord.classe"
      class="q-ma-lg"
      dense
      rounded
      outlined
      color="purple-4"
      bg-color="white"
    />
    <span>Vantagens</span>
    <q-separator color="white" />
    <q-input
      clearable
      v-model="editRecord.classPowers"
      class="q-ma-lg"
      dense
      rounded
      outlined
      color="purple-4"
      bg-color="white"
    />
    <q-input
      clearable
      v-model="editRecord.breedPowers"
      class="q-ma-lg"
      dense
      rounded
      outlined
      color="purple-4"
      bg-color="white"
    />
    <span>Desvantagens</span>
    <q-separator color="white" />
    <q-input
      clearable
      v-model="editRecord.classHandicap"
      class="q-ma-lg"
      dense
      rounded
      outlined
      color="purple-4"
      bg-color="white"
    />
    <q-input
      clearable
      v-model="editRecord.breedHandicap"
      class="q-ma-lg"
      dense
      rounded
      outlined
      color="purple-4"
      bg-color="white"
    />
    <span>Dados do Personagem</span>
    <q-separator color="white" />
    <q-input
      clearable
      v-model="editRecord.expertise"
      class="q-ma-lg"
      dense
      rounded
      outlined
      color="purple-4"
      bg-color="white"
    />
    <q-input
      clearable
      v-model="editRecord.history"
      class="q-ma-lg"
      dense
      rounded
      outlined
      color="purple-4"
      bg-color="white"
    />
    <span>Características</span>
    <q-separator color="white" />
    <div>
      <q-btn
        size="md"
        class="q-mt-lg q-mr-lg"
        color="red"
        label="Excluir"
        rounded
        @click="handleDeleteRecord(record.id)"
      />

      <q-btn
        size="md"
        class="q-mt-lg"
        color="green"
        label="Salvar"
        rounded
        type="submit"
        @click="handleEditRecord(record.id)"
      />
    </div>
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
    const {
      id,
      breed,
      name,
      age,
      gender,
      kit,
      classe,
      classPowers,
      breedPowers,
      classHandicap,
      breedHandicap,
      expertise,
      history,
    } = this.record
    this.editRecord = {
      id,
      breed,
      name,
      age,
      gender,
      kit,
      classe,
      classPowers,
      breedPowers,
      classHandicap,
      breedHandicap,
      expertise,
      history,
    }
  },
}
</script>

<style>
</style>
