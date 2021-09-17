<template>
  <a-layout-footer class="footer">
    {{ title }}
  </a-layout-footer>
</template>

<script>
export default {
  data() {
    return {
      title: ""
    };
  },
  props: {
    id: null
  },
  async fetch() {
    const response = await this.$prismic.api.getSingle("footer");

    if (!response) return;

    this.title = this.$prismic.asText(response.data.footer_title);
  }
};
</script>

<style>
.footer {
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 70px;
  /* background:#6cf; */
  text-align: center;
}
</style>
