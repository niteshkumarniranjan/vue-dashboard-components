<template>
  <div class="inline-block rounded-lg shadow-md bg-white relative" :class="{'w-full': fullWidth}">
    <slot />
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    fullWidth: Boolean
  }
}
</script>
