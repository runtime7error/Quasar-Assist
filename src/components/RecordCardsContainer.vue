<template>
  <div style="position: relative; top: 100px">
    <q-page-container class="row justify-start content-end">
      <div
        class="q-ma-lg"
        style="margin-right: 30px"
        :key="record.id"
        v-for="record in records"
        @click="handleClick(record)"
      >
        <q-card class="dialog-border null-card">
          <q-input
            :label="record.name"
            class="q-ma-lg"
            dense
            rounded
            outlined
            color="purple-4"
            bg-color="white"
            readonly
          />
          <q-input
            class="q-ma-lg"
            dense
            rounded
            outlined
            color="purple-4"
            bg-color="white"
            readonly
            :label="record.age"
          />
          <q-input
            :label="record.breed"
            class="q-ma-lg"
            dense
            rounded
            outlined
            color="purple-4"
            bg-color="white"
            readonly
          />
        </q-card>
      </div>
    </q-page-container>
  </div>
</template>

<script>
export default {
  props: ['records'],
  emits: ['showRecord'],
  methods: {
    handleClick(record) {
      this.$emit('showRecord', record)
    },
  },
}
</script>

<style>
</style>
