<template>
    <a-layout-header>
      <div class="logo" :style="{'background-image': `url(${logoUrl})`}"/>
      <a-menu class="menu"
        theme="dark"
        mode="horizontal"
        
        :style="{ lineHeight: '64px' }"
      >
        <a-menu-item key="1">
          nav 1
        </a-menu-item>
        <a-menu-item key="2">
          nav 2
        </a-menu-item>
        <a-menu-item key="3">
          nav 3
        </a-menu-item>
      </a-menu>
    </a-layout-header>
</template>
// :default-selected-keys="['2']"
<script>
export default {
  name: 'Header',
  data(){
    return {
      logoUrl: '',
      menuItems: []
    }
  },
  async fetch(){
    const result = await this.$prismic.api.getSingle('header');
    console.log(result.data);
    this.logoUrl = result.data.logo.url;
  }
}
</script>

<style scoped>
.menu {
  float: right;
}

.logo {
  width: 64px;
  height: 64px;
  float: left;

  background-size:     contain;
  background-repeat:   no-repeat;
  background-position: center center; 
  background-image: url('https://d33wubrfki0l68.cloudfront.net/6ff34ec8760318b99888ee4b75d1e265170a84b9/6479c/logos/nuxt.svg');
}
</style>