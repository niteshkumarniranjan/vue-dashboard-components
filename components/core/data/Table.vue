<template>
  <card fullWidth class="border overflow-hidden">
    <table class="table-auto w-full">
      <thead class="bg-gray-100 border-b">
        <tr class="select-none">
          <th v-if="selectable" class="px-4 py-4"></th>
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
          <th v-if="actionFunction" class="px-4 py-4"></th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="d in sortedData"
          :key="d.id"
          class="hover:bg-gray-100 border-b"
          :class="{ 'bg-gray-100': isSelected(d), 'cursor-pointer': selectable }"
          @click="onSelect(d)"
        >
          <td v-if="selectable" class="px-4 py-4">
            <CheckBox :checked="isSelected(d)" class="pointer-events-none" />
          </td>
          <td v-for="f in fields" :key="f" class="px-4 py-4">{{ d[f] }}</td>
          <td v-if="calcActions(d).length > 0" class="relative">
            <svg
              class="cursor-pointer"
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              @click="openMenu($event, d)"
            >
              <path d="M0 0h24v24H0z" fill="none" />
              <path
                d="M12 8c1.1 0 2-.9 2-2s-.9-2-2-2-2 .9-2 2 .9 2 2 2zm0 2c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2zm0 6c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"
              />
            </svg>
          </td>
        </tr>
      </tbody>
    </table>
    <portal to="menu">
      <transition
        enter-class="opacity-0 scale-90"
        enter-active-class="ease-out transition-fast"
        enter-to-class="opacity-100 scale-100"
        leave-class="opacity-100 scale-100"
        leave-active-class="ease-in transition-fastest"
        leave-to-class="opacity-0 scale-90"
      >
        <table-menu
          v-if="menu"
          @click="menuClick"
          @onClose="menu = false"
          :actions="selectedItemActions"
          :event="selectedItemEvent"
        />
      </transition>
    </portal>
  </card>
</template>

<script>
import Card from '../ui/Card'
import CheckBox from '../ui/CheckBox'
import TableMenu from './TableMenu'
var _ = require('lodash')

export default {
  props: {
    fields: Array,
    data: Array,
    selectable: Boolean,
    sortable: Boolean,
    sortedBy: String,
    actionFunction: Function
  },
  components: {
    Card,
    CheckBox,
    TableMenu
  },
  data: () => ({
    selected: [],
    sortableCol: '',
    asc: true,
    menu: false,
    selectedItem: null,
    selectedItemEvent: null
  }),
  computed: {
    sortedData() {
      const data = [...this.data]
      return _.orderBy(data, [this.sortableCol], [this.asc ? 'asc' : 'desc'])
    },
    selectedItemActions() {
      if (this.actionFunction && this.selectedItem) {
        return this.actionFunction(this.selectedItem)
      }
      return []
    }
  },
  mounted() {
    if (this.sortedBy) {
      let col = this.sortedBy
      if (this.sortedBy.startsWith('-')) {
        this.asc = false
        col = col.substr(1)
      }
      this.sortableCol = col
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
    },
    calcActions(item) {
      if (this.actionFunction) {
        const actions = this.actionFunction(item)
        return actions
      }
      return []
    },
    openMenu(e, d) {
      this.menu = false
      this.$nextTick(() => {
        this.selectedItemEvent = e
        this.selectedItem = d
        this.menu = true
      })
    },
    menuClick(action) {
      this.menu = false
      this.$emit(action, this.selectedItem)
    }
  }
}
</script>

<style>
.asc {
  transform: rotate(180deg);
}
</style>
