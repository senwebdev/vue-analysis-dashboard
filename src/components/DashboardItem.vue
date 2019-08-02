<template>
  <article
    class="dashboard-item"
    :data-columns="dataPackery.columns"
    :data-rows="dataPackery.rows"
  >
    <img v-if="img" :src="img" :alt="title" /> <slot></slot>
  </article>
</template>

<script>
export default {
  name: "DashboardItem",
  props: {
    component: Object,
    title: String,
    img: String,
    dataPackery: {
      type: Object,
      default: {
        columns: 1,
        rows: 2
      }
    }
  },
  data() {
    return {
      msg: "Welcome to Your Vue.js App"
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
