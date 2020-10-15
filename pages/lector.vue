<template lang='pug'>
  main
    h1 Aqui sera el lector de qr
    form.w-full.max-w-sm
      div.mb-6(class='md:flex md:items-center')
        div(class='md:w-1/3')
          label.block.text-gray-500.font-bold.mb-1.pr-4(class='md:text-right md:mb-0' for='inline-full-name')
            | Full Name
        div(class='md:w-2/3')
          input#inline-full-name.bg-gray-200.appearance-none.border-2.border-gray-200.rounded.w-full.py-2.px-4.text-gray-700.leading-tight(class='focus:outline-none focus:bg-white focus:border-purple-500' type='text' v-model='qrReading')
    p
      | Last result:
      b {{ decodedContent }}
    p.error
      | {{ error }}
    button(@click='openCamera')
      span {{ isShowingCamera ? 'Scanea un codigo QR' : 'Salir de escaneo' }}
    qrcode-stream(v-if='isShowingCamera' @decode='onDecode' @init='onInit')
    div
      pre {{ data }}
</template>

<script>

export default {
  data () {
    return {
      qrReading: '',
      data: {},
      decodedContent: '',
      error: '',
      isShowingCamera: false
    }
  },
  watch: {
    qrReading () {
      this.fetchDataQr()
    }
  },
  methods: {
    onDecode (content) {
      this.decodedContent = content
      this.fetchDataQr(content)
    },
    async fetchDataQr (content) {
      const data = await this.$axios.$get(content)
      this.data = data
    },
    async onInit (promise) {
      try {
        await promise
      } catch (error) {
        if (error.name === 'NotAllowedError') {
          this.error = 'ERROR: you need to grant camera access permisson'
        } else if (error.name === 'NotFoundError') {
          this.error = 'ERROR: no camera on this device'
        } else if (error.name === 'NotSupportedError') {
          this.error = 'ERROR: secure context required (HTTPS, localhost)'
        } else if (error.name === 'NotReadableError') {
          this.error = 'ERROR: is the camera already in use?'
        } else if (error.name === 'OverconstrainedError') {
          this.error = 'ERROR: installed cameras are not suitable'
        } else if (error.name === 'StreamApiNotSupportedError') {
          this.error = 'ERROR: Stream API is not supported in this browser'
        }
      }
    },
    openCamera () {
      this.isShowingCamera = !this.isShowingCamera
    }
  }
}
</script>

<style scoped></style>
