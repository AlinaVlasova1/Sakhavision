<script lang="ts">

import {defineComponent, reactive} from "vue";
import FolderComponent from "@/components/FolderComponent/FolderComponent.vue";
import {mockFolders} from "@/mock/mock-folders";

export default defineComponent({
  name: "ModalWindow",
  components: {FolderComponent},
  props: ['title', 'isModalWindowTriggered'],
  setup() {
    const selectedFolder = reactive({id: 0});
    return {
      selectedFolder
    }
  },
  methods: {
    mockFolders() {
      return mockFolders
    },
    activateButton() {
      this.closeWindow();
      this.$emit('select', this.selectedFolder);
    },
    closeWindow() {
      this.$emit('isModalWindowTriggered');
    },
    selectFolder(id: number) {
      this.selectedFolder.id = this.selectedFolder.id === id ? 0 : id;
    }
  }
})
</script>

<template>
  <div class="pop-up">
    <div class="pop-up-inner">
      <h1>{{title}}</h1>
      <div class="tree">
        <div v-for="(folder, index) in mockFolders()" :key="index">
          <FolderComponent :folder="folder" :selectedFolder="selectedFolder"
          @select-folder="selectFolder"></FolderComponent>
        </div>
      </div>
      <div class="buttons">
        <button @click="activateButton()">Ок</button>
        <button @click="closeWindow()">Закрыть</button>
      </div>
    </div>
  </div>
</template>

<style scoped>

  .pop-up {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    z-index: 99;
    background-color: rgba(10, 31, 56, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;

    .pop-up-inner {
      background-color: #80ADF0;
      height: 500px;
      width: 500px;
      position: relative;
      border-radius: 5px;

      .tree {
        width: 90%;
        margin-left: auto;
        margin-right: auto;
      }


      .buttons {
        position: absolute;
        bottom: 10%;
        top: auto;
        right: auto;
        left: auto;
        display: block;
        width: 100%;

        button {
          background-color: #2c3e50;
          color: white;
          border-radius: 5px;
          padding: 8px 10px;
          border: none;
        }

        button:first-child {
          margin-right: 10px;
        }
      }
    }
  }
</style>