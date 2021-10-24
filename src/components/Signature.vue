<template>
  <div class="signature">
    <VPerfectSignature
      :stroke-options="strokeOptions"
      ref="signaturePad"
      class="signaturePad"
      @onEnd="update"
    />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import VPerfectSignature, { StrokeOptions } from 'v-perfect-signature'

export default Vue.extend({
  props: {
    value: {
      type: Object,
      default() {
        return {}
      },
    },
  },
  components: {
    VPerfectSignature,
  },
  data: () => ({
    strokeOptions: {
      size: 16,
      thinning: 0.75,
      smoothing: 0.5,
      streamline: 0.5,
    } as StrokeOptions,
  }),
  watch: {
    value: {
      deep: true,
      handler() {
        this.load()
      },
    },
  },
  mounted() {
    this.load()
  },
  methods: {
    load() {
      if (this.value && this.value.hasOwnProperty('data')) {
        this.fromData(this.value.data)
      }
    },
    toDataURL() {
      return this.$refs.signaturePad.toDataURL()
    },
    toData() {
      return this.$refs.signaturePad.toData()
    },
    fromData(data) {
      console.log(data)
      if (!this.$refs) {
        console.error('ref not available yet')
        return
      }
      this.$refs.signaturePad.fromData(data)
    },
    clear() {
      this.$refs.signaturePad.clear()
      this.update()
    },
    update() {
      const data = this.toData()
      const dataURL = this.toDataURL()
      this.$emit('input', { data, dataURL })
    },
  },
})
</script>

<style scoped>
.signature {
  width: 100%;
  border-bottom: 1px solid gray;
}
.signaturePad {
  width: 100%;
}
</style>
