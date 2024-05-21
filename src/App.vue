<script setup lang="ts">
import { ref } from 'vue'
import Table from './Table.vue'
import Column from './Column.vue'

const items = ref([
  { id: 1, name: 'John Doe' },
  { id: 2, name: 'Jane Smith' }
])
</script>

<template>
  <div>
    <Table :items="items">
      <Column header="ID">
        <template #default="{ item }">
          {{ item.id }}
        </template>
      </Column>
      <Column header="Name">
        <template #default="{ item }">
          {{ item.name }}
        </template>
      </Column>
      <Column header="Name 2">
        <template #default="{ item }">
          {{ item.name }}
        </template>
      </Column>
      <Column>
        <template #header> static header </template>
        <template #default="{ item }"> Foobar </template>
      </Column>
    </Table>
  </div>
</template>
