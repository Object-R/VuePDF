<template>
  <div class="radio-group">
    <el-radio-group v-model="radio" @change="radioChange">
      <el-radio-button v-for="item in radios" :key="item" class="radio-button" :label="item" />
    </el-radio-group>
  </div>
  <div v-loading.fullscreen.lock="fullscreenLoading">
    <PdfPreview
      v-if="radio === radios[0]"
      :pdfUrl="pdf1"
      @pagesRendered="pagesRendered"
    ></PdfPreview>
    <PdfPreview v-else :pdfUrl="pdf2" @pagesRendered="pagesRendered"></PdfPreview>
  </div>
</template>

<script setup>
import PdfPreview from '@/components/PdfPreview.vue'
import pdf1 from '@/assets/2023碳排名分析报告（第二版）-压缩.pdf'
import pdf2 from '@/assets/企业碳计量与金融应用手册（第二版）-压缩.pdf'
import { ref } from 'vue'

const radios = [
  '2023碳排名分析报告',
  '企业碳计量与金融应用手册'
]

const radio = ref(radios[0])

const fullscreenLoading = ref(true)

const radioChange = () => {
  fullscreenLoading.value = true
}

const pagesRendered = () => {
  fullscreenLoading.value = false
}
</script>

<style scoped>
.radio-group {
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.radio-button {
  max-width: 48vw;
}
::v-deep(.el-radio-button__inner) {
  white-space: pre-wrap;
}
</style>