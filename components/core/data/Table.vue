<template>
  <card fullWidth class="border overflow-hidden">
    <table class="table-auto w-full">
      <thead class="bg-gray-100 border-b">
        <tr>
          <th v-if="selectable" class="px-4 py-4 border-b"></th>
          <th
            :class="{ 'cursor-pointer': sortable }"
            v-for="f in fields"
            :key="f"
            class="px-4 py-3 uppercase text-gray-700 text-sm font-medium text-left"
            @click="setSortabledCol(f)"
          >
            <span>{{ f }}</span>
            <svg
              class="w-4 inline-block opacity-0 transition-all transition-time-default transition-ease-in-out"
              style="vertical-align:text-top;"
              :class="{ 'opacity-100': sortable && sortableCol == f, 'asc': asc }"
              viewBox="0 0 20 20"
              focusable="false"
              aria-hidden="true"
            >
              <path d="M5 8l5 5 5-5z" fill-rule="evenodd" />
            </svg>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="d in sortedData"
          :key="d.id"
          class="hover:bg-gray-100"
          :class="{ 'bg-gray-100': isSelected(d), 'cursor-pointer': selectable }"
          @click="onSelect(d)"
        >
          <td v-if="selectable" class="px-4 py-4 border-b">
            <CheckBox :checked="isSelected(d)" />
          </td>
          <td v-for="f in fields" :key="f" class="px-4 py-4 border-b">{{ d[f] }}</td>
        </tr>
      </tbody>
    </table>
  </card>
</template>

<script>
import Card from '../ui/Card'
import CheckBox from '../ui/CheckBox'
var _ = require('lodash')

export default {
  props: {
    fields: Array,
    data: Array,
    selectable: Boolean,
    sortable: Boolean,
    sortedBy: String
  },
  components: {
    Card,
    CheckBox
  },
  data: () => ({
    selected: [],
    sortableCol: '',
    asc: true
  }),
  computed: {
    sortedData() {
      const data = [...this.data]
      return _.orderBy(data, [this.sortableCol], [this.asc ? 'asc' : 'desc'])
    }
  },
  mounted() {
    if (this.sortedBy) {
      let col = this.sortedBy
      if (this.sortedBy.startsWith('-')) {
        this.asc = false
        col = col.substr(1)
        this.sortedBy = col
      }
      this.sortableCol = this.sortedBy
    } else {
      this.sortableCol = this.fields[0]
    }
  },
  methods: {
    onSelect(d) {
      if (!this.selectable) return
      if (this.selected.includes(d.id)) {
        this.selected = this.selected.filter(id => id !== d.id)
      } else {
        this.selected.push(d.id)
      }
    },
    isSelected(d) {
      if (this.selected.includes(d.id)) return true
      return false
    },
    setSortabledCol(f) {
      if (this.sortable) {
        if (this.sortableCol === f) {
          this.asc = !this.asc
        } else {
          this.asc = true
          this.sortableCol = f
        }
      }
    }
  }
}
</script>

<style>
.asc {
  transform: rotate(180deg);
}
</style>
