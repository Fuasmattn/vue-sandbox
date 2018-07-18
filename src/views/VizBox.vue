<template>
  <div class="test">
    <h1>This is the VizBox 🤖</h1>
    <Sample title="YO"></Sample>
  </div>
</template>

<script lang="ts">
import Sample from '@/components/Sample.vue';
export default {
  name: 'VizBox',
  components: {
    Sample,
  },
};
</script>
