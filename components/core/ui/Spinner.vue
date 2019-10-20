<template>
  <span class="absolute inset-0 flex items-center justify-center">
    <div
      class="spinner flex"
      :class="{ 'w-6 h-6': size === 'small', 'w-10 h-10': size === 'default', 'w-24 h-24': size === 'large' }"
    >
      <div class="circle" :class="theme + ' ' + size"></div>
      <div class="circle" :class="theme + ' ' + size"></div>
      <div class="circle" :class="theme + ' ' + size"></div>
    </div>
  </span>
</template>

<script>
export default {
  name: 'Spinner',
  props: {
    size: {
      type: String,
      default: 'default',
      validator: v => {
        return ['default', 'small', 'large'].indexOf(v) !== -1
      }
    },
    theme: {
      type: String,
      default: 'dark',
      validator: v => {
        return ['dark', 'light'].indexOf(v) !== -1
      }
    }
  }
}
</script>

<style>
.spinner {
  position: relative;
  border-radius: 50%;
  box-sizing: border-box;
}

.spinner .circle {
  @apply absolute w-full h-full rounded-full;
  border: 1px solid transparent;
  border-left: 2px solid;
  transition: all 0.3s ease;
}

.spinner .circle.large {
  border-width: 2px;
  border-left-width: 3px;
}

.spinner .circle.light {
  border-left: 2px solid #fff;
}

.spinner .circle.dark {
  border-left: 2px solid #4a5568;
}

.spinner .circle:nth-child(1) {
  animation: rotate 1s ease infinite;
}
.spinner .circle:nth-child(2) {
  animation: rotateOpacity 1s ease infinite 0.1s;
}
.spinner .circle:nth-child(3) {
  animation: rotateOpacity 1s ease infinite 0.2s;
}

@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(1turn);
  }
}

@keyframes rotateOpacity {
  0% {
    transform: rotate(0deg);
    opacity: 0.1;
  }

  to {
    transform: rotate(1turn);
    opacity: 1;
  }
}
</style>
