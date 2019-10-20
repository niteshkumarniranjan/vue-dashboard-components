<template>
  <div>
    <div class="bg-gray-800 text-white py-4 px-6">
      <h1 class="text-2xl">Dashboard Components Mockups</h1>
    </div>
    <div class="container mx-auto text-grey-900">
      <div class="mt-6">
        <h4 class="text-xl">Separator:</h4>
        <v-divider class="mt-5 mb-4" />
        <v-divider text="with text" class="mt-5" />
      </div>
      <div class="mt-10">
        <h4 class="text-xl mb-6">Components:</h4>
        <v-divider text="Button" />
        <div class="mt-4 px-6">
          <v-button>Button</v-button>
          <v-button outline class="ml-3">Outlined</v-button>
          <v-button disabled class="ml-3">Disabled</v-button>
          <v-button loading class="ml-3">Loading</v-button>
          <v-button outline loading class="ml-3">Loading</v-button>
          <v-button class="ml-3" url="https://www.google.com" external>with &lt;a/&gt; tag</v-button>
          <v-divider text="size" class="mt-5 mb-4" />
          <v-button size="slim">Small</v-button>
          <v-button size="slim" outline class="ml-3">Small</v-button>
          <v-button class="ml-3">Default</v-button>
          <v-button outline class="ml-3">Default</v-button>
          <v-button size="large" class="ml-3">Large</v-button>
          <v-button outline size="large" class="ml-3">Large</v-button>
          <v-button loading size="large" class="ml-3">Large</v-button>
          <v-button full-width class="mt-4">Full-Width</v-button>
        </div>
      </div>
      <div class="mt-20">
        <v-divider text="Spinners" />
        <div class="mt-4 px-6">
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
        <v-divider text="Badges" class="mb-4" />
        <v-badge>5</v-badge>
        <v-badge class="ml-2">gray</v-badge>
        <v-badge color="green" class="ml-2">Success</v-badge>
        <v-badge color="yellow" class="ml-2">Waiting</v-badge>
        <v-badge color="red" class="ml-2">Wrong</v-badge>
      </div>
    </div>
  </div>
</template>

<script>
import Button from '@/components/ui/core/Button'
import Divider from '@/components/ui/core/Divider'
import Spinner from '@/components/ui/core/Spinner'
import Badge from '@/components/ui/core/Badge'

export default {
  components: {
    'v-button': Button,
    'v-divider': Divider,
    'v-spinner': Spinner,
    'v-badge': Badge
  }
}
</script>
