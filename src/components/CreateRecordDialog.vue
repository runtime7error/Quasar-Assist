<template>
  <div
    class="q-pa-md null-card dialog-border"
    style="max-width: 600px; width: 70%"
  >
    <q-form @submit="handleSave" @reset="handleClose" class="q-gutter-md">
      <q-card-section>
        <div class="text-h5 text-bold q-gutter-md">Criação de Ficha</div>
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
      <span class="text-h6 text-bold">Vantagens</span>
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
      <span class="text-h6 text-bold">Desvantagens</span>
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
      <span class="text-h6 text-bold">Dados do Personagem</span>
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
      <span class="text-h6 text-bold">Características</span>
      <q-separator color="white" />

      <!-- Força -->
      <div>
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
      <span class="text-h6 text-bold">Poder Mágico</span>
      <q-separator color="white" />
      <q-input
        readonly
        rounded
        dense
        class="q-mb-md"
        outlined
        autogrow
        color="purple-4"
        bg-color="white"
        placeholder="Mágias Conhecidas"
        v-model="record.knowMagic"
        type="textarea"
      />
      <q-select
        rounded
        dense
        class="q-mb-md"
        outlined
        multiple
        v-model="model"
        :options="options"
        bg-color="white"
        style="width: 250px"
      />
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
    options: ['Bola de Fogo', 'A Seta Infalível de Talude'],
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