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
    }
  }
})

</script>

<template>
<div class="main">
  <button @click="isModalWindowTriggered = true">Открыть</button>
</div>
  <ModalWindow v-if="isModalWindowTriggered"
               v-model="isModalWindowTriggered"
               :title="titleHeaderWindow"
               :isModalWindowTriggered="isModalWindowTriggered"
               @is-modal-window-triggered="isModalWindowTriggered = false" />
</template>

<style scoped>

  .main {
    display: flex;
    justify-content: center;
    vertical-align: center;
    height: 100%;
  }
</style>