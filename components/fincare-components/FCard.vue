<template lang="pug">
  v-card.fincare-card.rounded-xl.d-flex.flex-column.justify-start(
    v-if="disabled === false"
    @click="emitClick();"
    :min-height="height"
    :color="color"
    outlined
    )
    .px-4.pt-4.mb-auto
      v-row
        v-col(:cols="10")
          p.mb-0.font-weight-medium.text-h5(v-if="h5Title" :class="titleColorClass") {{ label }}
          p.mb-0.font-weight-medium.text-h6(v-else :class="titleColorClass") {{ label }}
        v-col.text-right(v-if="cornerIcon" :cols="2")
          //- Error: child cannot be removed
          v-btn(icon @click.stop="emitIconClick")
            client-only
              eva-icon(:name="cornerIconName" :fill="cornerIconColor"  width='32' height='32')
      p.mb-0.caption.font-weight-regular(:class="fontColorClass") {{ label2 }}
      p.mb-0.caption.font-weight-light(:class="fontColorClass") {{ label3 }}
      p.mb-0.font-16(:class="fontColorClass") {{ label4 }}
      slot(name="content")
    v-card-actions.px-4.pb-4
      slot(name="action")

  v-card.rounded-xl.d-flex.flex-column.justify-start(
    v-else
    :min-height="height"
    :color="color"
    outlined
    )
    .px-4.pt-4.mb-auto
      v-row
        v-col(:cols="10")
          p.mb-0.font-weight-medium.text-h6(:class="fontColorClass") {{ label }}
        v-col.text-right(v-if="cornerIcon" :cols="2")
          //- Error: child cannot be removed
          v-btn(icon)
            client-only
              eva-icon(:name="cornerIconName" :fill="cornerIconColor"  width='32' height='32')
      p.mb-0.caption.font-weight-regular(:class="fontColorClass") {{ label2 }}
      p.mb-0.caption.font-weight-light(:class="fontColorClass") {{ label3 }}
      p.mb-0.caption.font-weight-light(:class="fontColorClass") {{ label4 }}
      slot(name="content")
    v-card-actions.px-4.pb-4
      slot(name="action")
</template>
<script>
export default {
  name: 'FCard',
  props: {
    label: {
      type: String,
      default: null
    },
    label2: {
      type: String,
      default: null
    },
    label3: {
      type: String,
      default: null
    },
    label4: {
      type: String,
      default: null
    },
    height: {
      type: Number,
      default: 95
    },
    color: {
      type: String,
      default: null
    },
    cornerIcon: {
      type: String,
      default: null
    },
    disabled: {
      type: Boolean,
      default: false
    },
    h5Title: {
      type: Boolean,
      default: false
    },
    labelColorClass: {
      type: String,
      default: null
    }
  },
  data () {
    return {
      isIconClicked: false,
      cornerIconName: this.cornerIcon + '-outline',
      cornerIconColor: '#918679'
    }
  },
  computed: {
    fontColorClass () {
      if (this.color) {
        return 'white--text'
      } else {
        return 'secondary--text'
      }
    },
    titleColorClass () {
      if (this.labelColorClass) {
        return this.labelColorClass
      } else {
        return this.fontColorClass
      }
    }
  },
  methods: {
    emitClick () {
      this.$emit('click')
    },
    emitIconClick () {
      if (!this.isIconClicked) {
        this.cornerIconColor = `${this.$vuetify.theme.themes.light.primary}`
        this.cornerIconName = this.cornerIcon
        this.isIconClicked = true
      } else {
        this.cornerIconColor = `${this.$vuetify.theme.themes.light.brown}`
        this.cornerIconName = this.cornerIcon + '-outline'
        this.isIconClicked = false
      }
    }
  }
}
</script>

<style scoped>
.font-16 {
  font-size: 16px;
}
</style>
