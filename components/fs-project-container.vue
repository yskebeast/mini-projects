<template>
  <div class="fs-project-container">
    <h1 class="h1">{{ title }}</h1>
    <slot />
  </div>
</template>

<script>
export default {
  name: "fs-project-container",
  props: {
    title: String,
  },
};
</script>

<style lang="scss" scoped>
.fs-project-container {
  min-width: 1000px;
  width: 100%;
}
.h1 {
  text-align: center;
}
</style>
