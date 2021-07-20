<template>
  <q-layout view="lHh Lpr LFf" class="header">
    <!-- Navbar da página -->
    <Header @createRecord="toggleCreateRecordDialog" />

    <!-- Card caso não haja ficha criada -->
    <q-page-container v-if="records.length == 0" class="row text-h6">
      <div class="fixed-center" style="min-width: 200px">
        <q-card bordered dark class="null-card dialog-border">
          <q-card-section class="row justify-center">
            Parece que você não possui fichas cadastradas, clique no botão para
            criar uma agora mesmo!
            <q-btn
              rounded
              flat
              label="Criar"
              size="lg"
              style="margin-right: 5px"
              @click="toggleCreateRecordDialog"
            />
          </q-card-section>
        </q-card>
      </div>
    </q-page-container>

    <!-- Lista de cards -->
    <record-cards-container
      v-else
      :records="records"
      @showRecord="showRecord"
    />

    <!-- Diálogo de edição -->
    <q-page-container>
      <q-dialog v-model="displayEditRecordDialog">
        <edit-record-dialog
          :record="currentEditRecord"
          @deleteRecord="handleDeleteRecord"
          @editRecord="handleEditRecord"
        />
      </q-dialog>
    </q-page-container>

    <!-- Dialog de criação -->
    <q-page-container>
      <q-dialog v-model="displayCreateRecordDialog" persistent>
        <create-record-dialog
          v-if="displayCreateRecordDialog"
          @close="toggleCreateRecordDialog"
          @create="handleCreateRecord"
        />
      </q-dialog>
    </q-page-container>
  </q-layout>
</template>

<script>
// Lib
import Localbase from 'localbase'

// Helpers
import { generateUUID } from 'src/helpers/uuid'

// Components
import Header from 'src/components/Header.vue'
import CreateRecordDialog from 'src/components/CreateRecordDialog.vue'
import RecordCardsContainer from 'src/components/RecordCardsContainer.vue'
import EditRecordDialog from 'src/components/EditRecordDialog.vue'

let localbase = new Localbase('db')

export default {
  components: {
    Header,
    CreateRecordDialog,
    RecordCardsContainer,
    EditRecordDialog,
  },
  data: () => ({
    displayCreateRecordDialog: false,
    RecordCardsContainerteRecordDialog: false,
    displayEditRecordDialog: false,
    currentEditRecord: {},
    records: [],
    magics: [{ id: generateUUID(), name: 'bola de fogo' }],
  }),
  methods: {
    toggleCreateRecordDialog() {
      this.displayCreateRecordDialog = !this.displayCreateRecordDialog
    },
    toggleShowRecordDialog() {
      this.displayEditRecordDialog = !this.displayEditRecordDialog
    },
    showRecord(record) {
      this.currentEditRecord = record

      this.toggleShowRecordDialog()
    },
    async handleCreateRecord(data) {
      await localbase.collection('records').add({
        id: generateUUID(),
        ...data,
      })

      this.toggleCreateRecordDialog()
      this.fetchRecordsFromLocalbase()
    },
    async handleCreateMagicRecord(data) {
      if (this.magicRecords.length < 1) {
        let magics = {
          magic: this.magics,
        }
        await localbase.collection('magicRecords').add({ magics })
        this.fetchMagicRecordsFromLocalbase()
      }
    },
    async handleDeleteRecord({ id }) {
      await localbase
        .collection('records')
        .doc({
          id,
        })
        .delete()

      this.toggleShowRecordDialog()
      this.fetchRecordsFromLocalbase()
    },
    async handleEditRecord({ id, record }) {
      await localbase.collection('records').doc({ id }).update(record)

      this.toggleShowRecordDialog()
      this.fetchRecordsFromLocalbase()
    },
    async fetchRecordsFromLocalbase() {
      const records = await localbase.collection('records').get()
      this.records = records
    },
    async fetchMagicRecordsFromLocalbase() {
      const magicRecords = await localbase.collection('magicRecords').get()

      this.magicRecords = magicRecords
      this.handleCreateMagicRecord()
    },
  },
  mounted() {
    this.fetchMagicRecordsFromLocalbase()
    this.fetchRecordsFromLocalbase()
    // this.handleCreateMagicRecord()
    console.log('magias magicas', this.magicRecords)
  },
}
</script>
<style lang="scss">
@font-face {
  font-family: Montserrat;
  src: url('../fonts/montserrat-v15-latin-regular.woff') format('woff');
}

div {
  color: #ffffff;
}

.header {
  font-family: 'Montserrat';
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
  font-family: 'Montserrat';
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
