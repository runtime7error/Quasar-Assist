<template>
  <div
    class="q-pa-md null-card dialog-border"
    style="max-width: 600px; width: 70%"
  >
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
      <!-- Sexo -->
      <q-input
        dense
        rounded
        outlined
        color="purple-4"
        bg-color="white"
        placeholder="Sexo"
        lazy-rules
        v-model="record.gender"
        :rules="[
          value => (value && value.length > 0) || 'Sexo não pode ficar vazio !',
        ]"
        required
      />
      <!-- Kit -->
      <q-input
        dense
        rounded
        outlined
        color="purple-4"
        bg-color="white"
        placeholder="Kit"
        lazy-rules
        v-model="record.kit"
        :rules="[
          value => (value && value.length > 0) || 'Kit não pode ficar vazio !',
        ]"
        required
      />
      <!-- Classe -->
      <q-input
        class="q-mb-md"
        dense
        rounded
        outlined
        color="purple-4"
        bg-color="white"
        placeholder="Classe"
        v-model="record.classe"
      />
      <span>Vantagens</span>
      <q-separator color="white" />
      <!-- Vantagens de Raça -->
      <q-input
        dense
        rounded
        outlined
        color="purple-4"
        bg-color="white"
        placeholder="Vantagens de Raça"
        lazy-rules
        v-model="record.classPowers"
        :rules="[
          value =>
            (value && value.length > 0) ||
            'Vantagens de raça não pode ficar vazio !',
        ]"
        required
      />
      <!-- Vantagens de Classe -->
      <q-input
        class="q-mb-md"
        dense
        rounded
        outlined
        color="purple-4"
        bg-color="white"
        placeholder="Vantagens de Classe"
        v-model="record.breedPowers"
      />
      <span>Desvantagens</span>
      <q-separator color="white" />
      <!-- Desvantagens de Classe -->
      <q-input
        dense
        rounded
        outlined
        color="purple-4"
        bg-color="white"
        placeholder="Desvantagens de Classe"
        v-model="record.classHandicap"
      />
      <span></span>
      <!-- Desvantagens de Raça -->
      <q-input
        class="q-mb-md"
        dense
        rounded
        outlined
        color="purple-4"
        bg-color="white"
        placeholder="Desvantagens de Raça"
        v-model="record.breedHandicap"
      />
      <span>Dados do Personagem</span>
      <q-separator color="white" />
      <!-- Perícias -->
      <q-input
        dense
        rounded
        outlined
        color="purple-4"
        bg-color="white"
        placeholder="Perícias"
        v-model="record.expertise"
      />
      <span />
      <!-- História -->
      <q-input
        rounded
        dense
        class="q-mb-md"
        outlined
        autogrow
        color="purple-4"
        bg-color="white"
        placeholder="História"
        v-model="record.history"
        type="textarea"
      />
      <span>Características</span>
      <q-separator color="white" />
      <div>
        <q-btn size="md" class="q-mt-lg q-mr-lg" color="red" label="Cancelar" rounded type="reset" />

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
      gender: '',
      kit: '',
      classe: '',
      classPowers: '',
      breedPowers: '',
      classHandicap: '',
      breedHandicap: '',
      expertise: '',
      history: '',
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
