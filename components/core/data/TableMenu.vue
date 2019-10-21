<template>
  <div
    class="absolute bg-white shadow rounded py-1 origin-top-right"
    style="min-width: 160px;"
    ref="menu"
    :style="`top: ${event.pageY}px;left: ${event.pageX - (width + 16)}px;`"
  >
    <div
      v-for="item in actions"
      :key="item.name"
      @click="$emit('click', item.action)"
      class="px-4 py-3 leading-tight cursor-pointer hover:bg-gray-200 text-sm"
    >{{ item.name }}</div>
  </div>
</template>

<script>
export default {
  name: 'TableMenu',
  props: {
    actions: {
      type: Array,
      required: true
    },
    event: {
      required: true
    }
  },
  data() {
    return {
      width: 0
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.width = this.$refs.menu.clientWidth
    })

    const listner = $event => {
      if (
        $event.target !== this.$refs.menu &&
        $event.target !== this.event.target
      ) {
        this.$emit('onClose')
      }
    }

    document.addEventListener('click', listner)

    this.$on('hook:beforeDestroy', () => {
      document.removeEventListener('click', listner)
    })
  }
}
</script>
