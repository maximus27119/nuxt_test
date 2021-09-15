<template>
  <a-layout class="app">
    <component v-for="component of components" :is="getComponentName(component.type)" :key="component.type" :id="component.id"/>
  </a-layout>
</template>

<script>
export default {
  methods: {
    getComponentName(compName){
      // console.log(this.components);
      return `app-${compName}`.toLowerCase();
    }
  },
  async asyncData({ $prismic, error }) {
    const response = await $prismic.api.getSingle("home_page");

    const result = Object.values(response.data)
    // console.log(result);
    if (result){
      return { 
        components: result.filter(e => e.id)
      }
    }else{
      console.log("error");
      error({ statusCode: 404, message: 'Page not found' })
    }
  },
}
</script>

<style scoped>
  .app{
    min-height: 100vh;
  }
</style>