<template>
  <div id='webviewer' ref='viewer'></div>
</template>

<script>
import { ref, onMounted } from 'vue'
import WebViewer from '@compdfkit_pdf_sdk/webviewer'

export default {
  name: 'WebViewer',

  setup() {
    const viewer = ref(null)
    let docViewer = null

    onMounted(() => {
      WebViewer.init({
        path: '/',
        pdfUrl: './example/developer_guide_web.pdf',
        license: '<Input your license here>'
      }, viewer.value).then((instance) => {
        docViewer = instance.docViewer

        docViewer.addEvent('documentloaded', async () => {
          console.log('document loaded')
        })
      })
    })

    return {
      viewer,
      docViewer
    }
  }
}
</script>

<style>
#webviewer {
  height: 100vh;
  overflow: hidden;
}
</style>
