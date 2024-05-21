<template>
  <table>
    <thead>
      <tr>
        <th v-for="(column, index) in columns" :key="index">
          <component v-if="column.vnode.children.header" :is="column.vnode.children.header" />
          <template v-else>{{ column.header }}</template>
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
  vnode: any
}

const props = defineProps<{ items: any[] }>()
const columns = ref<Column[]>([])

function registerColumn(column: Column) {
  console.log(' => registerColumn', column)
  const idx = columns.value.findIndex((c) => c.instance.uid === column.instance.uid)
  if (idx >= 0) {
    columns.value[idx] = column
  } else {
    columns.value.push(column)
  }
}

Object.assign(window, { columns })

provide('registerColumn', registerColumn)
</script>
