<template>
  <div class="flex items-center">
    <span v-if="text" class="pr-3 text-sm uppercase font-semibold text-indigo-500">{{ text }}</span>
    <span class="flex-1 bg-gray-400" style="height: 2px"></span>
  </div>
</template>

<script>
export default {
  props: {
    text: String
  }
}
</script>
