<template>
  <vue-pdf-app class="pdf-app" :title="true" :pdf="props.pdfUrl" @pagesRendered="pagesRendered" :config="config"></vue-pdf-app>
</template>

<script setup>
import VuePdfApp from "vue3-pdf-app";
import "vue3-pdf-app/dist/icons/main.css";
const props = defineProps({
  pdfUrl: String
})

const emit = defineEmits(['pagesRendered'])

const pagesRendered = () => {
  emit('pagesRendered')
}

const config ={
  toolbar: {
    toolbarViewerRight: {
      // download: false,
      // print: false,
      openFile: false
    }
  }
}

</script>

<style scoped>
.pdf-app {
  height: calc(100vh - 60px);
}
::v-deep(.toolbar) {
  z-index: 1000 !important;
}
</style>