<template>
  <div>
    <label v-if="label" class="block font-medium mb-2">{{ label }}</label>
    <div @click="onClick" :class="parentClasses">
      <div
        v-if="prefix"
        class="px-3 py-2 bg-gray-100 border-r-2 font-medium text-gray-800 rounded-l transition-all transition-time-default transition-ease-in-out"
        :class="{ 'border-indigo-500': focus }"
        :id="realId+'Prefix'"
      >{{ prefix}}</div>
      <div class="px-2 py-2 w-full">
        <dynamic-tag
          :tag="multiline ? 'textarea' : 'input'"
          :name="name"
          :id="realId"
          :type="type"
          :disabled="disabled"
          :readonly="readOnly"
          :autofocus="autoFocus"
          :value="value"
          :placeholder="placeholder"
          :on="{
            change: handleChange,
            focus: onFocus,
            blur: onBlur,
          }"
          :style="{ height: (multiline && height) ? height+'px' : null }"
          :autocomplete="autoComplete"
          class="bg-transparent focus:outline-none w-full h-full"
          ref="input"
        ></dynamic-tag>
      </div>
      <div
        v-if="suffix"
        class="px-3 py-2 bg-gray-100 border-l-2 font-medium text-gray-800 rounded-r transition-all transition-time-default transition-ease-in-out"
        :class="{ 'border-indigo-500': focus }"
        :id="realId+'Suffix'"
      >{{ suffix }}</div>
    </div>
  </div>
</template>

<script>
import DynamicTag from './DynamicTag'

export default {
  name: 'TextField',
  model: {
    prop: 'value',
    event: 'change'
  },
  props: {
    prefix: String,
    suffix: String,
    placeholder: String,
    value: [String, Number],
    label: String,
    disabled: Boolean,
    readOnly: Boolean,
    autoFocus: Boolean,
    multiline: [Boolean, Number],
    error: [Boolean, String],
    type: String,
    name: String,
    id: String,
    autoComplete: Boolean,
    max: Number,
    maxLength: Number,
    min: Number,
    minLength: Number
  },
  components: {
    DynamicTag
  },
  computed: {
    parentClasses() {
      const _ = [
        'border-2 rounded flex transition-all transition-time-default transition-ease-in-out'
      ]

      if (this.disabled) {
        _.push('pointer-events-none bg-gray-100')
      }

      if (this.focus) {
        _.push('bg-white border-indigo-500')
      } else {
        _.push('cursor-text')
      }
      return _
    }
  },
  data() {
    return {
      height: null,
      focus: false,
      realId: ''
    }
  },
  mounted() {
    this.realId = this.id || 'DashboardTextFiel' + this._uid
  },
  methods: {
    onFocus() {
      this.focus = true
      this.$emit('focus')
    },
    onBlur() {
      this.focus = false
      this.$emit('blur')
    },
    onClick() {
      this.$refs.input.focus()
    },
    handleChange(e) {
      console.log('newValue', e)
      var target = e.target || e.srcElement
      this.$emit('change', target.value)
    }
  }
}
</script>
