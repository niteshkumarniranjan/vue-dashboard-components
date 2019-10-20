<template>
  <card fullWidth class="border overflow-hidden">
    <table class="table-auto w-full">
      <thead class="bg-gray-100 border-b">
        <tr>
          <th v-if="selectable" class="px-4 py-4 border-b"></th>
          <th
            v-for="f in fields"
            :key="f"
            class="px-4 py-3 uppercase text-gray-700 text-sm font-medium text-left"
          >{{ f }}</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="d in data"
          :key="d.id"
          class="cursor-pointer hover:bg-gray-100"
          :class="{ 'bg-gray-100': isSelected(d) }"
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

export default {
  props: {
    fields: Array,
    data: Array,
    selectable: Boolean
  },
  components: {
    Card,
    CheckBox
  },
  data: () => ({
    selected: []
  }),
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
    }
  }
}
</script>
