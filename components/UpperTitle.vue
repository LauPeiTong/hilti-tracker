<template lang="pug">
  v-row.py-4.pl-4.upper-title(dense :class="titleClass")
    //- v-col.text-center(:cols="2")
    //-   f-icon(
    //-     v-if="back === true"
    //-     :icon-name="'arrow-ios-back-outline'"
    //-     :icon-fill="titleClass == 'dark-background'? 'white' : iconColor"
    //-     @click="emitBack()"
    //-   )
    v-col(:cols="10")
      h3.font-weight-medium(:class="textColor") {{ title }}
    v-col.text-center(:cols="2")
      f-icon(
        :icon-name="icon"
        :icon-fill="rightIconColor ?? iconColor"
        :border="border"
        @click="emitClick()"
      )

</template>

<script>
import { mapGetters, mapActions } from 'vuex'
import FIcon from './fincare-components/FIcon.vue'

export default {
  name: 'UpperTitle',
  components: {
    FIcon
  },
  props: {
    title: {
      type: String,
      default: null
    },
    titleClass: {
      type: String,
      default: null
    },
    icon: {
      type: String,
      default: null
    },
    back: {
      type: Boolean,
      default: false
    },
    border: {
      type: Boolean,
      default: false
    },
    rightIconColor: {
      type: String,
      default: null
    }
  },
  data () {
    return {
    }
  },
  computed: {
    ...mapGetters({
    }),
    textColor () {
      if (this.titleClass === 'dark-background') {
        return 'white--text'
      } else {
        return 'secondary--text'
      }
    },
    iconColor () {
      if (this.titleClass === 'dark-background') {
        return 'white'
      } else {
        return 'primary'
      }
    }
  },
  methods: {
    ...mapActions({
    }),
    emitBack () {
      this.$emit('goBack')
    },
    emitClick () {
      this.$emit('clicked')
    }
  }
}
</script>

<style lang="scss" scoped>
.upper-title {
  position: absolute !important;
  top: 0;
  width: 100%;
  border-radius: 0px 0px 25px 25px;
  z-index: 100;
}

.dark-background {
  background-color: #D2051E;
}
</style>
