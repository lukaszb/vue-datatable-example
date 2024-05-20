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
      <template v-slot:id="{ item }">
        {{ item.id }}
      </template>
      <template v-slot:name="{ item }">
        {{ item.name }}
      </template>
      <Column header="ID" key="id"></Column>
      <Column header="Name" key="name"></Column>
    </Table>
  </div>
</template>
