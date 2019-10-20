<template>
  <card fullWidth class="border overflow-hidden">
    <table class="table-auto w-full">
      <thead class="bg-gray-100 border-b">
        <tr>
          <th v-for="f in 4" :key="f" class="px-4 py-3 text-center">
            <span class="skeleton-th"></span>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="d in 3" :key="d">
          <td v-for="f in 4" :key="f" class="px-4 py-4 border-b text-center">
            <span class="skeleton-td"></span>
          </td>
        </tr>
      </tbody>
    </table>
  </card>
</template>

<script>
import Card from '../ui/Card'

export default {
  name: 'SkeletonTable',
  components: {
    Card
  }
}
</script>

<style>
.skeleton-th {
  display: inline-block;
  height: 0.8rem;
  max-width: 8rem;
  width: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  will-change: opacity;
  position: relative;
  animation: skeletonShimmerAnimation 0.8s linear infinite alternate;
}

.skeleton-th::after {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  display: block;
  background-color: #dfe3e8;
  border-radius: 3px;
}

.skeleton-td {
  display: inline-block;
  height: 0.5rem;
  max-width: 12rem;
  width: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  will-change: opacity;
  position: relative;
  animation: skeletonShimmerAnimation 0.8s linear infinite alternate;
}

.skeleton-td::after {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  display: block;
  background-color: #dfe3e8;
  border-radius: 3px;
}
</style>
