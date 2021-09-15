<template>
    <a-layout-header>
      <div class="logo" />
      <a-menu
        theme="dark"
        mode="horizontal"
        :default-selected-keys="['2']"
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

<script>
export default {
  name: 'Header'
}
</script>

<style scoped>
.logo {
  width: 64px;
  height: 64px;
  /* background: rgba(255, 255, 255, 0.2); */
  /* margin: 16px 28px 16px 0; */
  vertical-align: center;
  /* margin: 10px 2px; */
  float: left;

  background-size:     contain;                      /* <------ */
  background-repeat:   no-repeat;
  background-position: center center; 
  background-image: url('https://d33wubrfki0l68.cloudfront.net/6ff34ec8760318b99888ee4b75d1e265170a84b9/6479c/logos/nuxt.svg');
}
</style>