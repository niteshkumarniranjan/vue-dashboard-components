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
        return ['small', 'medium', 'large', 'extraLarge'].indexOf(s) > -1
      }
    }
  },
  computed: {
    classes() {
      var r = ['skeleton-display-text__display-text']

      r.push(`skeleton-display-text--size-${this.size}`)

      return r
    }
  }
}
</script>

<style>
.skeleton-display-text--extraLarge {
  height: 3.2rem;
}

.skeleton-display-text--size-large {
  height: 2.8rem;
}

.skeleton-display-text--size-medium {
  height: 2.4rem;
}

.skeleton-display-text--size-small {
  height: 2.2rem;
}

.skeleton-display-text__display-text {
  max-width: 12rem;
  width: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  will-change: opacity;
  position: relative;
  animation: skeletonShimmerAnimation 0.8s linear infinite alternate;
}

.skeleton-display-text__display-text::after {
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
