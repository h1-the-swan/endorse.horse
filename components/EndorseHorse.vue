<template>
  <div>
    <h1>{{ props.service_or_item }}</h1>
    
  </div>
</template>

<script lang="ts" setup>
const props = defineProps<{
  episode_date: string;
  service_or_item: string;
  endorser: string;
  category: string;
  notes?: string;
}>()
</script>

<style>

</style>