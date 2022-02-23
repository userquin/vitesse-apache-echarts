<script setup lang="ts">
const AsyncChartComponent = typeof window !== 'undefined'
  ? defineAsyncComponent(() => import('../components/ChartComponent.vue'))
  : undefined
</script>
<template>
  <client-only>
    <template v-if="AsyncChartComponent">
      <component :is="AsyncChartComponent" />
    </template>
  </client-only>
</template>
