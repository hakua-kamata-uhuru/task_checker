<script setup>
import { computed } from 'vue'
import GenreBody from './GenreBody.vue';
import TaskBody from './TaskBody.vue'

//子コンポーネントのTaskBodyの処理を親コンポーネントのToDoListに伝達する役割
const emit = defineEmits(['close-modal'])  

// closeModal関数を追加
const closeModal = () => {
  emit('close-modal')
}

const props = defineProps({
  body: String
})

const component = computed(() =>  {
  return props.body === 'taskBody' ? TaskBody: GenreBody
})
</script>

<template>
  <Modal v-model="showModal">
    <component :is="component" @close-modal="closeModal" />
  </Modal>
</template>

<style>
.vm {
  height: 75vh;
  padding: 2vw 10vw;
  text-align: center;
  overflow-y: auto;
}
</style>