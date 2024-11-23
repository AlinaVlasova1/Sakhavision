<script lang="ts">

import {defineComponent} from "vue";
import FolderComponent from "@/components/FolderComponent/FolderComponent.vue";
import {mockFolders} from "@/mock/mock-folders";

export default defineComponent({
  name: "ModalWindow",
  components: {FolderComponent},
  props: ['title', 'isModalWindowTriggered'],
  data() {
    return {
      idSelectedFolder: 0
    }
  },
  setup() {
    // const idSelectedFolder = ref(0);
    // return {
    //   idSelectedFolder
    // }
  },
  methods: {
    mockFolders() {
      return mockFolders
    },
    activatedButton() {
      this.closeWindow();
    },
    closeWindow() {
      this.$emit('isModalWindowTriggered');
    },
    selectFolder(value: number) {
      console.log('value',value);
      if (this.idSelectedFolder !== value) {
        this.idSelectedFolder = value;
      } else {
        this.idSelectedFolder = 0;
      }

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
          <FolderComponent :folder="folder" :idSelectedFolder="idSelectedFolder"
          @select-folder="selectFolder()"></FolderComponent>
        </div>
      </div>
      <div class="buttons">
        <button @click="activatedButton()">Ок</button>
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
    background-color: wheat;
    height: 500px;
    width: 500px;
    position: relative;


    .buttons {
      position: absolute;
      bottom: 10%;
      top: auto;
      right: auto;
      left: auto;
      display: block;
      width: 100%;
    }
  }
}
</style>