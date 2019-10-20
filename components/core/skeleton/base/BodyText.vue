<template>
  <dynamic-tag :tag="element" class="skeleton-body-text__skeleton-body-text-container">
    <span v-for="i in lines" :key="i" class="skeleton-body-text__body-text"></span>
  </dynamic-tag>
</template>

<script>
import DynamicTag from '../../ui/DynamicTag'

export default {
  props: {
    element: {
      type: String,
      default: 'p'
    },
    lines: {
      type: Number,
      default: 1
    }
  },
  components: {
    DynamicTag
  }
}
</script>

<style>
.skeleton-body-text__skeleton-body-text-container {
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  will-change: opacity;
  animation: skeletonShimmerAnimation 0.8s linear infinite alternate;
}

.skeleton-body-text__body-text {
  height: 0.8rem;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  will-change: opacity;
  position: relative;
  display: block;
  margin-bottom: 6px;
}

.skeleton-body-text__body-text:not(:only-child):last-child {
  width: 80%;
}

.skeleton-body-text__body-text::after {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  display: block;
  background-color: #dfe3e8;
  border-radius: 3px;
}
</style>
