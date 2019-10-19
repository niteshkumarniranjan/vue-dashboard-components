<template>
  <div class="container mx-auto py-4 text-grey-900">
    <div>
      <h1 class="text-2xl">Dashboard Components Mockups</h1>
    </div>
    <div class="mt-6">
      <v-divider text="Button" />
      <div class="mt-4 px-4">
        <v-button>Button</v-button>
        <v-button outline class="ml-3">Outlined</v-button>
        <v-button disabled class="ml-3">Disabled</v-button>
        <v-button loading class="ml-3">Loading</v-button>
        <v-button outline loading class="ml-3">Loading</v-button>
        <v-button class="ml-3" url="https://www.google.com" external>with &lt;a/&gt; tag</v-button>
        <v-divider text="size" class="mt-5 mb-4" />
        <v-button size="slim">Small</v-button>
        <v-button class="ml-3">Default</v-button>
        <v-button class="ml-3" size="large">Large</v-button>
      </div>
    </div>
    <div class="mt-20">
      <v-divider text="Spinners" />
      <div class="mt-4 px-4">
        <div class="flex">
          <div class="w-6 h-6 relative">
            <v-spinner size="small" />
          </div>
          <div class="ml-8 w-10 h-10 relative">
            <v-spinner />
          </div>
          <div class="ml-8 w-24 h-24 relative">
            <v-spinner size="large" />
          </div>
        </div>
        <v-divider text="Light variant" class="mt-5 mb-4" />
        <div class="flex mt-4">
          <div class="w-6 h-6 relative bg-gray-700">
            <v-spinner theme="light" size="small" />
          </div>
          <div class="ml-8 w-10 h-10 relative bg-gray-700">
            <v-spinner theme="light" />
          </div>
          <div class="ml-8 w-24 h-24 relative bg-gray-700">
            <v-spinner theme="light" size="large" />
          </div>
        </div>
      </div>
    </div>
    <div class="mt-20">
      <h4 class="text-xl">Separator</h4>
      <v-divider class="mt-5 mb-4" />
      <v-divider text="with text" class="mt-5 mb-4" />
    </div>
  </div>
</template>

<script>
import Button from '@/components/ui/basic/Button'
import Divider from '@/components/ui/basic/Divider'
import Spinner from '@/components/ui/basic/Spinner'

export default {
  components: {
    'v-button': Button,
    'v-divider': Divider,
    'v-spinner': Spinner
  }
}
</script>
