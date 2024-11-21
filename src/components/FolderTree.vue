<template>
  <ul class="base">
    <li v-for="folder in folders" :key="folder.id">
      <div
        @click="handleClick(folder.id)"
        :class="{ selected: selectedFolder === folder.id }"
      >
        {{ folder.name }}
        <span v-if="folder.children.length">
          [{{ isOpen(folder.id) ? '-' : '+' }}]
        </span>
      </div>
      <FolderTree
        v-if="folder.children.length && isOpen(folder.id)"
        :folders="folder.children"
        :selectedFolder="selectedFolder"
        @selectFolder="selectFolder"
      />
    </li>
  </ul>
</template>

<script setup lang="ts">
import { ref, type PropType } from "vue";

interface Folder {
  id: number;
  name: string;
  children: Folder[];
}

defineProps({
  folders: {
    type: Array as PropType<Folder[]>,
    required: true,
  },
  selectedFolder: {
    type: Number,
    required: false,
  },
});

const emit = defineEmits(["selectFolder"]);

const openFolders = ref<Set<number>>(new Set());

const isOpen = (id: number) => openFolders.value.has(id);

const toggleFolder = (id: number) => {
  if (isOpen(id)) openFolders.value.delete(id);
  else openFolders.value.add(id);
};

const handleClick = (id: number) => {
  selectFolder(id);
  toggleFolder(id);
};

const selectFolder = (id: number) => {
  emit("selectFolder", id);
};
</script>

<style scoped>
.base {
  color: red;
}
.selected {
  font-weight: bold;
  color: blue;
  cursor: pointer;
}
</style>
