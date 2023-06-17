<template>
  <div class="the-sidebar">
    <h1 class="h1">プロジェクト名</h1>
    <ul class="list">
      <li class="item" v-for="project in projectList" :key="project.name">
        <nuxt-link :to="project.url">{{ project.name }}</nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
import projectList from "~/data/project-list";

export default {
  name: "the-sidebar",
  computed: {
    projectList: () => projectList,
  },
};
</script>

<style lang="scss" scoped>
.the-sidebar {
  width: 300px;
  background-color: gray;
  flex-shrink: 0;
}

.h1 {
  font-size: 1.35rem;
  text-align: center;
}

.item {
  margin-bottom: 1rem;
}
</style>
