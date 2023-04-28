<template lang="pug">
  v-btn.fincare-icon(icon :color="buttonColor" :width="width" :height="height" :to="to" :border="border" :class="borderClass")
    client-only
      eva-icon(:name="iconName" :fill="iconFill" @click="emitClick" :width="iconWidth" :height="iconHeight")
</template>
<script>
export default {
  name: 'FIcon',
  props: {
    iconName: {
      type: String,
      default: null
    },
    iconFill: {
      type: String,
      default: null
    },
    disabled: {
      type: Boolean,
      default: false
    },
    border: {
      type: Boolean,
      default: false
    },
    width: {
      type: Number,
      default: 27
    },
    height: {
      type: Number,
      default: 27
    },
    to: {
      type: String,
      default: null
    }
  },
  computed: {
    buttonColor () {
      let color = this.iconFill

      if (this.color) { color = this.color }
      if (this.disabled) { color = 'darkGrey' }

      return color
    },
    borderClass () {
      if (this.border) {
        return 'woreer-icon-border pt-1'
      } else {
        return ''
      }
    },
    iconWidth () {
      if (this.border) {
        return this.width - 7
      } else {
        return this.width
      }
    },
    iconHeight () {
      if (this.border) {
        return this.height - 7
      } else {
        return this.height
      }
    }
  },
  methods: {
    emitClick () {
      this.$emit('click')
    }
  }
}
</script>

<style scoped>
:deep(.btn-icon) {
  display: flex;
  width: 0.8rem;
  margin-right: 0.5rem;
}

.theme--light.v-btn.v-btn--disabled.v-btn--has-bg {
  background-color: #848484 !important;
  color: #C1C1C1 !important;
}

:deep(.v-btn__content) {
  opacity: 1 !important;
  letter-spacing: -0.011em;
}

.fincare-icon-border {
  border: 2px solid white;
}
</style>
