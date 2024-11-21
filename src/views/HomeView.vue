<template>
  <div>
    <button @click="openModal">Открыть</button>
    <ModalWindow
      v-if="isModalOpen"
      :isOpen="isModalOpen"
      title="Выберите папку"
      @close="closeModal"
      @confirm="confirmSelection"
    >
      <FolderTree
        :folders="mockFolders"
        :selectedFolder="selectedFolder"
        @selectFolder="setSelectedFolder"
      />
    </ModalWindow>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import ModalWindow from '@/components/ModalWindow.vue'
import FolderTree from '@/components/FolderTree.vue'

const mockFolders = [
  {
    id: 1,
    name: 'Папка 1',
    children: [
      { id: 2, name: 'Папка 1.1', children: [] },
      { id: 3, name: 'Папка 1.2', children: [{ id: 4, name: 'Папка 1.2.1', children: [] }] },
    ],
  },
  { id: 5, name: 'Папка 2', children: [] },
]

const isModalOpen = ref(false)
const selectedFolder = ref<number | 0>(0)

const openModal = () => {
  isModalOpen.value = true
}
const closeModal = () => {
  isModalOpen.value = false
}
const confirmSelection = () => {
  console.log('Выбрана папка ID:', selectedFolder.value)
  closeModal()
}
const setSelectedFolder = (id: number) => {
  selectedFolder.value = id
}
</script>
