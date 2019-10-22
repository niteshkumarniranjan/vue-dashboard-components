<template>
  <dynamic-tag
    :tag="url? 'a': 'button'"
    :on="{
      click: onClick,
      blur: onBlur,
      focus: onFocus
    }"
    :type="submit? 'submit' : 'button'"
    :class="classes"
    :href="url"
    :disabled="isDisabled"
    :target="external? '_blank' : ''"
    class="appearance-none"
  >
    <span v-if="loading">
      <spinner
        class="rounded-lg"
        :class="{'bg-indigo-700': !outline, 'bg-indigo-100': outline}"
        size="small"
        :theme="outline? 'dark' : 'light'"
        accessibility-label="Loading"
      />
    </span>
    <span v-if="icon" class="bt__icon">
      <polaris-icon :source="realIcon"></polaris-icon>
    </span>
    <span v-if="$slots.default" :class="{ 'leading-tight' : url && size === 'large' }">
      <slot></slot>
    </span>
  </dynamic-tag>
</template>

<script>
import DynamicTag from './DynamicTag'
import Spinner from './Spinner'

export default {
  name: 'Button',
  components: {
    DynamicTag,
    Spinner
  },
  props: {
    url: String,
    outline: Boolean,
    plain: Boolean,
    disabled: Boolean,
    loading: Boolean,
    size: {
      type: String,
      default: 'default',
      validator: v => {
        return ['default', 'slim', 'large'].indexOf(v) !== -1
      }
    },
    external: Boolean,
    fullWidth: Boolean,
    submit: Boolean,
    icon: String,
    iconOnly: Boolean
  },
  computed: {
    isDisabled() {
      return this.disabled || this.loading
    },
    classes() {
      const _ = [
        'relative inline-flex items-center align-middle justify-center leading-none font-semibold border-2 border-transparent uppercase tracking-wide rounded no-underline focus:outline-none focus:shadow-outline transition-all transition-time-default transition-ease-in-out'
      ]

      switch (this.size) {
        case 'default':
          _.push('px-6 py-3')
          break
        case 'slim':
          _.push('py-1 px-4 h-8')
          break
        case 'large':
          _.push('h-12 px-6 py-3')
      }

      if (this.isDisabled && !this.loading) {
        _.push('pointer-events-none opacity-50')
      }

      if (this.loading) {
        _.push('pointer-events-none')
      }

      if (this.fullWidth) {
        _.push('w-full')
      }

      if (this.plain) {
        _.push('hover:bg-indigo-200 active:bg-indigo-300')
      } else if (this.outline) {
        _.push('border-indigo-800 hover:bg-indigo-200 active:bg-indigo-300')
      } else {
        _.push(
          'bg-indigo-700 text-white shadow-md hover:bg-indigo-600 active:bg-indigo-800'
        )
      }

      return _
    }
  },
  methods: {
    onClick(e) {
      if (this.disabled) return
      if (this.submit) return true
      this.$emit('click', e)
    },
    onFocus(e) {
      this.$emit('focus', e)
    },
    onBlur(e) {
      this.$emit('blur', e)
    }
  }
}
</script>

<style>
</style>
