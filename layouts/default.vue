<template>
  <div class="antialiased">
    <nuxt />
    <portal-target name="menu"></portal-target>
  </div>
</template>

<style>
html {
  font-family: 'Inter', sans-serif;
}

body {
  @apply .bg-gray-100;
}
</style>
