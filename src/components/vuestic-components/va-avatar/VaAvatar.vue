<template>
  <div
    class="va-avatar"
    ref="avatar"
    :style="computedStyle"
  >
    <slot>
      <img
        v-if="src"
        :src="src"
      >
      <va-icon
        v-else-if="icon"
        :name="icon"
      />
    </slot>
  </div>
</template>

<script>
import { SizeMixin } from '../../../mixins/SizeMixin'
import { ColorThemeMixin } from '../../../services/ColorThemePlugin'
import { makeContextablePropsMixin } from '../../context-test/context-provide/ContextPlugin'
import VaIcon from '../va-icon/VaIcon'

const contextConfigMixin = makeContextablePropsMixin({
  color: {
    type: String,
    default: 'info',
  },
  textColor: {
    type: String,
    default: 'white',
  },
  square: {
    type: Boolean,
    default: false,
  },
  icon: {
    type: String,
    default: '',
  },
  src: {
    type: String,
    default: null,
  },
  fontSize: {
    type: String,
    default: '',
  },
})

export default {
  name: 'VaAvatar',
  mixins: [SizeMixin, ColorThemeMixin, contextConfigMixin],
  components: {
    VaIcon,
  },
  computed: {
    computedStyle () {
      return {
        color: this.computeInvertedColor(this.c_textColor),
        backgroundColor: this.colorComputed,
        borderRadius: this.c_square ? 0 : '50%',
        fontSize: this.c_fontSize,
        width: this.sizeComputed,
        minWidth: this.sizeComputed, // We only define width because common use case would be flex row, for column we expect user to set appropriate styling externally.
        height: this.sizeComputed,
      }
    },
  },
}
</script>

<style lang="scss">
.va-avatar {
  align-items: center;
  display: inline-flex;
  justify-content: center;
  line-height: normal;
  position: relative;
  text-align: center;
  vertical-align: middle;

  img,
  svg {
    border-radius: inherit;
    display: inline-flex;
    height: inherit;
    width: inherit;
    margin: auto;
  }
}
</style>
