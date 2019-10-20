<template>
  <span :class="classes">
    <slot />
  </span>
</template>

<script>
export default {
  name: 'Badge',
  props: {
    color: {
      type: String,
      default: 'default',
      validator: v => {
        return ['default', 'green', 'red', 'yellow'].indexOf(v) !== -1
      }
    }
  },
  computed: {
    classes() {
      const _ = [
        'inline-block px-2 py-1 leading-none rounded-full text-sm font-medium tracking-wide'
      ]

      switch (this.color) {
        default:
          _.push('bg-gray-200 text-gray-800')
          break
        case 'red':
          _.push('bg-red-200 text-red-800')
          break
        case 'green':
          _.push('bg-green-200 text-green-800')
          break
        case 'yellow':
          _.push('bg-yellow-200 text-yellow-800')
          break
      }

      return _
    }
  }
}
</script>
