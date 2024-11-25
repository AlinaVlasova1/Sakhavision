<script lang="ts">

import ModalWindow from "@/components/ModalWindow/ModalWindow.vue";
import {defineComponent} from "vue";

export default defineComponent({
  name: "MainPage",
  components: {ModalWindow},
  data() {
    return {
      isModalWindowTriggered: false as boolean,
      titleHeaderWindow: 'Заголовок модального окна' as string,
      idSelectedFolderInModalWindow: null as number | null
    }
  },
  methods: {
    select(id: number) {
      this.idSelectedFolderInModalWindow = id;
    }
  }
})

</script>

<template>
<div class="main">
  <button class="open-modal" @click="isModalWindowTriggered = true">Открыть</button>
</div>
  <ModalWindow v-if="isModalWindowTriggered"
               v-model="isModalWindowTriggered"
               :title="titleHeaderWindow"
               :isModalWindowTriggered="isModalWindowTriggered"
               @is-modal-window-triggered="isModalWindowTriggered = false" @select="select" />
</template>

<style scoped>

  .main {
    height: 100%;
    position: relative;

    .open-modal {
      position: absolute;
      top: 45%;
      background-color: #2c3e50;
      color: white;
      border-radius: 5px;
      padding: 8px 10px;
    }
  }
</style>