<template>
  <ul>
    <learning-resource
      v-for="(resource, index) in resources"
      :key="index"
      :title="resource.title"
      :description="resource.description"
      :link="resource.link"
    >
    </learning-resource>
  </ul>
</template>

<script>
import LearningResource from './LearningResource';

export default {
  name: 'StoredResources',
  props: {},
  inject: ['resources'],
  components: {
    LearningResource,
  },
  data() {
    return {};
  },
  methods: {},
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>