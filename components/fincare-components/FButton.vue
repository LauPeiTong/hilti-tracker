<template lang="pug">
  v-btn.wecan-button.text-none.rounded-lg(
    elevation="0"
    :block="block"
    :dark="dark"
    :min-height="buttonMinHeight"
    :color="buttonColor"
    :plain="plain"
    :outlined="outlined"
    :disabled="disabled"
    @click="emitClick"
    :to="to"
  )

    client-only
      eva-icon.ma-0(v-if="iconOnly" :name="iconName" :fill="disabled? '#C1C1C1' : iconFill")
      .d-flex.flex-column.px-2.align-center(v-else)
        .btn-icon.mr-3(v-if="iconName")
          eva-icon(:name="iconName" :fill="disabled? '#C1C1C1' : iconFill")
        span {{label}}
      .right-action
        slot(name="action")

</template>
<script>
export default {
  name: 'FButton',
  props: {
    label: {
      type: String,
      default: null
    },
    color: {
      type: String,
      default: null
    },
    iconName: {
      type: String,
      default: null
    },
    iconFill: {
      type: String,
      default: null
    },
    to: {
      type: String,
      default: null
    },
    outlined: {
      type: Boolean,
      default: false
    },
    block: {
      type: Boolean,
      default: true
    },
    dark: {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    },
    activeClass: {
      type: String,
      default: null
    },
    plain: {
      type: Boolean,
      default: false
    },
    borderless: {
      type: Boolean,
      default: false
    },
    iconOnly: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    buttonMinHeight () {
      if (this.iconName) {
        return '64px'
      } else if (this.iconName && !this.label) {
        return '10px'
      } else {
        return '48px'
      }
    },
    buttonColor () {
      let color = 'primary'

      if (this.color) { color = this.color }
      if (this.disabled) { color = 'darkGrey' }

      return color
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
</style>
