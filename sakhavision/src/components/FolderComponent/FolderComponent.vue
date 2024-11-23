<script lang="ts">

import {defineComponent} from "vue";

export default defineComponent({
  name: "FolderComponent",
  props: ['folder', 'idSelectedFolder'],
  data() {
    return {
      isArrowTriggered: false as boolean,
      isSelect: false,
    }
  },
  methods: {
    selectedFolder() {
      this.$emit('selectFolder', this.folder.id)
    },
    selectFolderChild(value: number) {
      this.$emit('selectFolder', value)
    }
  }
})
</script>

<template>
  <div class="folder-container">
    <img class="down-arrow"
         v-if="folder.children.length > 0"
         @click="isArrowTriggered = !isArrowTriggered" src="../../assets/down-arrow.svg" alt="down-arrow" />
    <span class="name-folder">{{folder.name}}</span>
    <input class="check-box" type="checkbox" v-model="isSelect" @click="selectedFolder()"
           :disabled="(idSelectedFolder.id !== 0) && (idSelectedFolder.id !== folder.id)">
    <div class="children" v-if="isArrowTriggered && (folder.children.length > 0)">
      <div v-for="(child, index) in folder.children" :key="index">
        <FolderComponent :folder="child"
                         :idSelectedFolder="idSelectedFolder"
                         @select-folder="selectFolderChild"></FolderComponent>
      </div>
    </div>
  </div>
</template>

<style scoped>

  .folder-container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;

    .down-arrow {
      height: 15px;
      width: auto;
      grid-column-start: 1;
      grid-column-end: 1;
      grid-row-start: 1;
      grid-row-end: 1;
    }

    .name-folder {
      grid-column-start: 2;
      grid-column-end: 2;
      grid-row-start: 1;
      grid-row-end: 1;
    }

    .check-box {
      grid-column-start: 3;
      grid-column-end: 3;
      grid-row-start: 1;
      grid-row-end: 1;
    }

    .children {
      display: grid;
      grid-column-start: 1;
      grid-column-end: 4;
      grid-row-start: 2;
      grid-row-end: 2;
    }
  }

</style>