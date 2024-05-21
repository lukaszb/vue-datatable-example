<script setup lang="ts">
import { defineProps, inject, onMounted, onUpdated, getCurrentInstance } from 'vue'

const props = defineProps<{ header?: string }>()
const registerColumn = inject<Function>('registerColumn')

const register = () => {
  const instance = getCurrentInstance()
  if (instance && instance.vnode && registerColumn) {
    registerColumn({
      header: props.header,
      vnode: instance.vnode,
      instance
    })
  }
}

onMounted(() => {
  register()
})

onUpdated(() => {
  register()
})
</script>
