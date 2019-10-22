<template>
  <div class="inline-block leading-none align-middle">
    <label
      :for="realId"
      class="inline-flex items-center select-none"
      :class="{ 'pointer-events-none': disabled }"
    >
      <div
        class="w-5 h-5 relative rounded-full border border-indigo-700 cursor-pointer flex items-center justify-center shadow"
        :class="{ 'bg-indigo-700': checked, 'bg-indigo-300 border-2 opacity-50': disabled }"
      >
        <span class="w-2 h-2 rounded-full" :class="{'bg-white': checked}"></span>
        <input
          type="radio"
          :id="realId"
          :name="name"
          :value="value"
          class="opacity-0 absolute inset-0 cursor-pointer"
          role="radio"
          :checked="checked"
          :disabled="disabled"
          @change="onChange"
          @focus="onFocus"
          @blur="onBlur"
        />
      </div>
      <span v-if="label" class="ml-2">{{ label }}</span>
    </label>
  </div>
</template>

<script>
export default {
  name: 'RadioButton',
  model: {
    prop: 'modelValue',
    event: 'change'
  },
  props: {
    value: {},
    modelValue: {},
    label: String,
    labelHidden: Boolean,
    id: String,
    name: String,
    disabled: Boolean
  },
  computed: {
    checked() {
      return this.modelValue === this.value
    }
  },
  data: () => ({
    realId: ''
  }),
  mounted() {
    this.realId = this.id || 'Checkbox' + this._uid
  },
  methods: {
    onChange(e) {
      this.$emit('change', this.value)
    },
    onFocus(e) {
      this.$emit('focus', e)
    },
    onBlur(e) {
      this.$emit('blur', e)
    }
  }
}
</script>
