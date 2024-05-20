<template>
  <table>
    <thead>
      <tr>
        <th v-for="(column, index) in columns" :key="index">
          {{ column.header }}
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(item, index) in items" :key="index">
        <td v-for="(column, columnIndex) in columns" :key="columnIndex">
          <component :is="column.vnode.children.default" :item="item" />
        </td>
      </tr>
    </tbody>
    <slot />
  </table>
</template>

<script setup lang="ts">
import { defineProps, ref, provide } from 'vue'

interface Column {
  header: string
  slotName: string
  vnode: any
}

const props = defineProps<{ items: any[] }>()
const columns = ref<Column[]>([])

function registerColumn(column: Column) {
  console.log(' => registerColumn', column)
  columns.value.push(column)
}

Object.assign(window, { columns })

provide('registerColumn', registerColumn)
</script>
