<template>
  <div class="pb-20">
    <div class="bg-gray-800 text-white py-4 px-6 shadow-lg">
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
          <v-button plain class="ml-3">Plain Button</v-button>
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
      <div class="mt-20">
        <v-divider text="Card" class="mb-4" />
        <v-card class="px-4 py-6">Basic Card</v-card>
        <v-card fullWidth class="px-4 py-6 mt-4">
          This is a
          <pre class="inline">fullWidth </pre>card
        </v-card>
      </div>
      <div class="mt-20">
        <v-divider text="TextField" class="mb-4" />
        <v-card fullWidth class="px-4 py-6">
          <v-text-field v-model="text" value="Nitesh Kumar Niranjan" label="Name" />
          <v-text-field multiline label="Multiline" class="mt-4" />
          <div class="mt-4 flex">
            <div class="w-1/2 pr-2">
              <v-text-field
                v-model="text"
                label="With Prefix"
                prefix="github.com/"
                placeholder="username"
              />
            </div>
            <div class="w-1/2 pl-2">
              <v-text-field
                v-model="text"
                label="With Suffix"
                placeholder="placeholder"
                suffix="/user"
              />
            </div>
          </div>
          <v-text-field label="Read only" read-only value="readonly" class="mt-4" />
          <v-text-field label="Disabled" disabled value="Disabled" class="mt-4" />
        </v-card>
      </div>
      <div class="mt-20">
        <v-divider text="CheckBox" class="mb-4" />
        <v-card fullWidth class="px-4 py-6">
          <v-checkbox label="Default" v-model="checked" />
          <v-checkbox label="Checked" checked class="ml-3" />
          <v-checkbox label="Indeterminate" class="ml-3" checked="indeterminate" />
          <v-checkbox disabled label="Disabled" class="ml-3" />
          <v-checkbox disabled checked label="Disabled" class="ml-3" />
        </v-card>
      </div>
      <div class="mt-20">
        <v-divider text="Radio Button" class="mb-4" />
        <v-card fullWidth class="px-4 py-6">
          <v-radio-button name="option" label="Option 1" v-model="option" value="1" />
          <v-radio-button name="option" label="Option 2" v-model="option" value="2" class="ml-3" />
          <v-radio-button
            name="option"
            label="Option 1 (Disabled)"
            v-model="option"
            value="1"
            disabled
            class="ml-3"
          />
          <v-radio-button
            name="option"
            label="Option 2 (Disabled)"
            v-model="option"
            value="2"
            disabled
            class="ml-3"
          />
        </v-card>
      </div>
      <div class="mt-20">
        <v-divider text="Data Table" class="mb-4" />
        <v-card fullWidth class="px-4 py-6">
          <v-table :fields="['name', 'role', 'location', 'status']" :data="tableData" />
          <v-divider text="with select" class="my-4" />
          <v-table
            selectable
            :fields="['id', 'name', 'role', 'location', 'status']"
            :data="tableData"
          />
          <v-divider text="sortable" class="my-4" />
          <v-table
            sortable
            sortedBy="-status"
            :fields="['id', 'name', 'role', 'location', 'status']"
            :data="tableData"
          />
        </v-card>
      </div>
    </div>
  </div>
</template>

<script>
import Button from '@/components/core/ui/Button'
import Divider from '@/components/core/ui/Divider'
import Spinner from '@/components/core/ui/Spinner'
import Badge from '@/components/core/ui/Badge'
import Card from '@/components/core/ui/Card'
import TextField from '@/components/core/ui/TextField'
import Table from '@/components/core/data/Table'
import CheckBox from '@/components/core/ui/CheckBox'
import RadioButton from '@/components/core/ui/RadioButton'

export default {
  components: {
    'v-button': Button,
    'v-divider': Divider,
    'v-spinner': Spinner,
    'v-badge': Badge,
    'v-card': Card,
    'v-text-field': TextField,
    'v-table': Table,
    'v-checkbox': CheckBox,
    'v-radio-button': RadioButton
  },
  data: () => ({
    tableData: [
      {
        id: 1,
        name: 'Nitesh Kumar Niranjan',
        role: 'Front End Developer',
        location: 'Delhi, India',
        status: 'C'
      },
      {
        id: 2,
        name: 'Rahul Roy',
        role: 'Full Stack Develoepr',
        location: 'Delhi, India',
        status: 'B'
      },
      {
        id: 3,
        name: 'Prakash Bharti',
        role: 'Senior Front End Developer',
        location: 'Delhi, India',
        status: 'C'
      }
    ],
    checked: false,
    option: '1',
    text: ''
  })
}
</script>
