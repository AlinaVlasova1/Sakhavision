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
  setup(props) {
    console.log('props.idSelectedFolder', props.idSelectedFolder)
  },
  methods: {
    selectedFolder() {
      this.$emit('selectFolder', this.folder.id)
    }
  }
})
</script>

<template>
  <div class="folder-container">
    <img class="down-arrow"
         v-if="folder.children.length > 0"
         @click="isArrowTriggered = !isArrowTriggered" src="../../assets/down-arrow.svg" alt="down-arrow" />
    <span>{{folder.name}}</span>
    <input type="checkbox" v-model="isSelect" @click="selectedFolder()"
           :disabled="(idSelectedFolder !== 0) && (idSelectedFolder !== folder.id)">
    <div v-if="isArrowTriggered && (folder.children.length > 0)">
      <div v-for="(child, index) in folder.children" :key="index">
        <FolderComponent :folder="child" :idSelectedFolder="idSelectedFolder"></FolderComponent>
      </div>
    </div>
  </div>
</template>

<style scoped>

  .folder-container {


    .down-arrow {
      height: 20px;
      width: auto;
    }
  }

</style>