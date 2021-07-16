<template>
  <div class="q-pa-md null-card dialog-border dialog-responsive" >
    <q-form @submit="handleSave" @reset="handleClose" class="q-gutter-md">
      <q-card-section>
        <div class="text-h5 text-bold q-gutter-md">Criação de Ficha</div>
      </q-card-section>
      <!-- Nome -->
      <div
        class="q-pa-md"
        style="
          min-width: 200px;
          max-width: 400px;
          margin-left: auto;
          margin-right: auto;
        "
      >
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
            value =>
              (value && value.length > 0) || 'Nome não pode ficar vazio!',
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
            value =>
              (value && value.length > 0) || 'Raça não pode ficar vazio !',
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
            value =>
              (value && value.length > 0) || 'Sexo não pode ficar vazio !',
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
            value =>
              (value && value.length > 0) || 'Kit não pode ficar vazio !',
          ]"
          required
        />
        <!-- Classe -->
        <q-input
          dense
          rounded
          outlined
          color="purple-4"
          bg-color="white"
          placeholder="Classe"
          v-model="record.classe"
        />
        <!-- Vantagens de Raça -->
        <span class="text-h6 text-bold tableMenu">Vantagens</span>
        <q-separator class="q-mb-md" color="white" />
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
          dense
          rounded
          outlined
          color="purple-4"
          bg-color="white"
          placeholder="Vantagens de Classe"
          v-model="record.breedPowers"
        />

        <!-- Desvantagens de Classe -->
        <span class="text-h6 text-bold tableMenu">Desvantagens</span>
        <q-separator class="q-mb-md" color="white" />
        <q-input
          dense
          rounded
          outlined
          color="purple-4"
          bg-color="white"
          placeholder="Desvantagens de Classe"
          v-model="record.classHandicap"
        />

        <!-- Desvantagens de Raça -->
        <q-input
          class="q-mt-md"
          dense
          rounded
          outlined
          color="purple-4"
          bg-color="white"
          placeholder="Desvantagens de Raça"
          v-model="record.breedHandicap"
        />

        <!-- Perícias -->
        <span class="text-h6 text-bold tableMenu">Dados do Personagem</span>
        <q-separator class="q-mb-md" color="white" />
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
          class="q-mt-md"
          outlined
          autogrow
          color="purple-4"
          bg-color="white"
          placeholder="História"
          v-model="record.history"
          type="textarea"
        />
        <!-- Força -->
        <div>
          <span class="text-h6 text-bold">Características</span>
          <q-separator color="white" />
          <q-field dark borderless v-model="record.StrValue">
            <template v-slot:control>
              <div class="self-center no-outline" tabindex="0">
                Força : {{ record.StrValue }}
              </div>
            </template>
            <template v-slot:append>
              <q-btn
                color="white"
                flat
                round
                :disable="record.StrValue < 1"
                icon="remove_circle"
                @click.stop="record.StrValue -= 1"
              />
              <q-btn
                color="white"
                flat
                round
                icon="add_circle"
                @click.stop="record.StrValue += 1"
              />
            </template>
          </q-field>

          <!-- Habilidade -->
          <q-field dark borderless v-model="record.HabValue">
            <template v-slot:control>
              <div class="self-center no-outline" tabindex="0">
                Habilidade : {{ record.HabValue }}
              </div>
            </template>
            <template v-slot:append>
              <q-btn
                color="white"
                flat
                round
                :disable="record.HabValue < 1"
                icon="remove_circle"
                @click.stop="record.HabValue -= 1"
              />
              <q-btn
                color="white"
                flat
                round
                icon="add_circle"
                @click.stop="record.HabValue += 1"
              />
            </template>
          </q-field>

          <!-- Resistência -->
          <q-field dark borderless v-model="record.ResValue">
            <template v-slot:control>
              <div class="self-center no-outline" tabindex="0">
                Resistência : {{ record.ResValue }}
              </div>
            </template>
            <template v-slot:append>
              <q-btn
                color="white"
                flat
                round
                :disable="record.ResValue < 1"
                icon="remove_circle"
                @click.stop="record.ResValue -= 1"
              />
              <q-btn
                color="white"
                flat
                round
                icon="add_circle"
                @click.stop="record.ResValue += 1"
              />
            </template>
          </q-field>

          <!-- Poder de Fogo -->
          <q-field dark borderless v-model="record.PdfValue">
            <template v-slot:control>
              <div class="self-center no-outline" tabindex="0">
                Poder de Fogo : {{ record.PdfValue }}
              </div>
            </template>
            <template v-slot:append>
              <q-btn
                color="white"
                flat
                round
                :disable="record.PdfValue < 1"
                icon="remove_circle"
                @click.stop="record.PdfValue -= 1"
              />
              <q-btn
                color="white"
                flat
                round
                icon="add_circle"
                @click.stop="record.PdfValue += 1"
              />
            </template>
          </q-field>
        </div>
        <span class="text-h6 text-bold">Poder Mágico</span>
        <q-separator color="white" />
        <div>
          <!-- Focus de Fogo -->
          <q-field dark borderless v-model="record.FireValue">
            <template v-slot:control>
              <div class="self-center no-outline" tabindex="0">
                Fogo : {{ record.FireValue }}
              </div>
            </template>
            <template v-slot:append>
              <q-btn
                color="white"
                flat
                round
                :disable="record.FireValue < 1"
                icon="remove_circle"
                @click.stop="record.FireValue -= 1"
              />
              <q-btn
                color="white"
                flat
                round
                icon="add_circle"
                @click.stop="record.FireValue += 1"
              />
            </template>
          </q-field>

          <!-- Focus de Terra -->
          <q-field dark borderless v-model="record.EarthValue">
            <template v-slot:control>
              <div class="self-center no-outline" tabindex="0">
                Terra : {{ record.EarthValue }}
              </div>
            </template>
            <template v-slot:append>
              <q-btn
                color="white"
                flat
                round
                :disable="record.EarthValue < 1"
                icon="remove_circle"
                @click.stop="record.EarthValue -= 1"
              />
              <q-btn
                color="white"
                flat
                round
                icon="add_circle"
                @click.stop="record.EarthValue += 1"
              />
            </template>
          </q-field>
          <!-- Focus de Luz -->
          <q-field dark borderless v-model="record.LightValue">
            <template v-slot:control>
              <div class="self-center no-outline" tabindex="0">
                Luz : {{ record.LightValue }}
              </div>
            </template>
            <template v-slot:append>
              <q-btn
                color="white"
                flat
                round
                :disable="record.LightValue < 1"
                icon="remove_circle"
                @click.stop="record.LightValue -= 1"
              />
              <q-btn
                color="white"
                flat
                round
                icon="add_circle"
                @click.stop="record.LightValue += 1"
              />
            </template>
          </q-field>
          <!-- Focus de Trevas -->
          <q-field dark borderless v-model="record.DarkValue">
            <template v-slot:control>
              <div class="self-center no-outline" tabindex="0">
                Trevas : {{ record.DarkValue }}
              </div>
            </template>
            <template v-slot:append>
              <q-btn
                color="white"
                flat
                round
                :disable="record.DarkValue < 1"
                icon="remove_circle"
                @click.stop="record.DarkValue -= 1"
              />
              <q-btn
                color="white"
                flat
                round
                icon="add_circle"
                @click.stop="record.DarkValue += 1"
              />
            </template>
          </q-field>
        </div>
        <span class="text-h6 text-bold tableMenu">Poder Mágico</span>
        <q-separator class="q-mb-md" color="white" />
        <q-input
          readonly
          rounded
          dense
          outlined
          autogrow
          color="purple-4"
          bg-color="white"
          placeholder="Mágias Conhecidas"
          v-model="record.selectdOptions"
          type="textarea"
        />
        <q-select
          class="q-mt-md"
          rounded
          dense
          outlined
          bg-color="white"
          options-dark
          color="purple-4"
          v-model="record.selectdOptions"
          :options="options"
          multiple
        />
      </div>
      <div>
        <q-btn
          size="md"
          class="q-mt-lg q-mr-lg"
          color="red"
          label="Cancelar"
          rounded
          type="reset"
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
    </q-form>
  </div>
</template>

<script>
export default {
  emits: ['create', 'close'],
  data: () => ({
    display: true,
    options: ['Magia 1', 'Magia 2'],
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
      HabValue: 0,
      StrValue: 0,
      ResValue: 0,
      PdfValue: 0,
      FireValue: 0,
      EarthValue: 0,
      WindValue: 0,
      LightValue: 0,
      DarkValue: 0,
      selectedOptions: [],
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