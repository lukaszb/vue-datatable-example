<script setup lang="ts">
import { defineProps, inject, onMounted, getCurrentInstance } from 'vue'

const props = defineProps<{ header: string }>()
const registerColumn = inject<Function>('registerColumn')

onMounted(() => {
  const instance = getCurrentInstance()
  if (instance && instance.vnode && instance.vnode.key && registerColumn) {
    const slotName = instance.vnode.key as string
    registerColumn({
      header: props.header,
      slotName: slotName
    })
  }
})
</script>
