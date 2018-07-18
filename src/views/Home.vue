<template>
  <div class="home">
    <Landing msg="Data/InfoViz Sandbox"/>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Landing from '@/components/Landing.vue'; // @ is an alias to /src

export default Vue.extend({
  name: 'home',
  components: {
    Landing,
  },
});
</script>
