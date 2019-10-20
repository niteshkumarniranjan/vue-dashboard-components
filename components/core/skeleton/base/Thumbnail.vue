<template>
  <div :class="classes" />
</template>

<script>
export default {
  props: {
    size: {
      type: String,
      default: 'medium',
      validate(s) {
        return ['small', 'medium', 'large'].indexOf(s) > -1
      }
    }
  },
  computed: {
    classes() {
      var r = ['skeleton-thumbnail__thumbnail']

      r.push(`skeleton-thumbnail--size-${this.size}`)

      return r
    }
  }
}
</script>

<style>
.skeleton-thumbnail--size-large {
  height: 3.2rem;
  width: 3.2rem;
}

.skeleton-thumbnail--size-medium {
  height: 2.8rem;
  width: 2.8rem;
}

.skeleton-thumbnail--size-small {
  height: 2.4rem;
  width: 2.4rem;
}

.skeleton-thumbnail__thumbnail {
  max-width: 12rem;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  will-change: opacity;
  position: relative;
  animation: skeletonShimmerAnimation 0.8s linear infinite alternate;
}

.skeleton-thumbnail__thumbnail::after {
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
