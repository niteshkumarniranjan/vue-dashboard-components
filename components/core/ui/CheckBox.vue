<template>
  <div class="inline-block leading-none align-middle">
    <label
      :for="realId"
      class="inline-flex items-center select-none"
      :class="{ 'pointer-events-none': disabled }"
    >
      <div
        class="w-5 h-5 relative rounded border border-gray-700 cursor-pointer flex items-center justify-center shadow"
        :class="{ 'bg-gray-700': checked, 'bg-gray-300 border-2 opacity-50': disabled }"
      >
        <template v-if="checked">
          <svg
            v-if="checked === 'indeterminate'"
            class="w-5 h-5 text-white fill-current relative pointer-events-none"
            viewBox="0 0 20 20"
            focusable="false"
            aria-hidden="true"
          >
            <path d="M15 9H5a1 1 0 1 0 0 2h10a1 1 0 1 0 0-2" fill-rule="evenodd" />
          </svg>
          <svg
            v-else
            class="w-5 h-5 text-white fill-current relative pointer-events-none"
            viewBox="0 0 20 20"
            focusable="false"
            aria-hidden="true"
          >
            <path
              d="M8.315 13.859l-3.182-3.417a.506.506 0 0 1 0-.684l.643-.683a.437.437 0 0 1 .642 0l2.22 2.393 4.942-5.327a.437.437 0 0 1 .643 0l.643.684a.504.504 0 0 1 0 .683l-5.91 6.35a.437.437 0 0 1-.642 0"
            />
          </svg>
        </template>
        <input
          type="checkbox"
          :id="realId"
          :name="name"
          :value="value"
          class="opacity-0 absolute inset-0 cursor-pointer z-10"
          :aria-invald="error == true"
          role="checkbox"
          :aria-checked="indeterminate ? 'mixed' : (checked ? 'true' : null)"
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
  name: 'CheckBox',
  model: {
    prop: 'checked',
    event: 'change'
  },
  props: {
    label: String,
    labelHidden: Boolean,
    checked: {
      type: [Boolean, String],
      default: false,
      validator(v) {
        return v && typeof v === 'string' ? v === 'indeterminate' : true
      }
    },
    id: String,
    name: String,
    value: String,
    error: [Boolean, String],
    disabled: Boolean
  },
  computed: {
    indeterminate() {
      return this.checked == 'indeterminate'
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
      var target = e.target || e.srcElement
      this.$emit('change', target.checked)
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
