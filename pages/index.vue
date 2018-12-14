<template>
  <div>
    <img src="~static/logo.png" alt>
    <ul class="diss">
      <li>
        <nuxt-link :to="{name:'index'}">home</nuxt-link>
        <nuxt-link :to="{name:'asyncData'}">asyncData</nuxt-link>
        <nuxt-link :to="{name:'about'}">about</nuxt-link>
        <nuxt-link :to="{name:'news', params:{newsId:3306}}">news</nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
// import AppLogo from "~/components/AppLogo.vue";

export default {
  components: {
    // AppLogo
  }
};
</script>

<style>
.diss {
  width: 300px;
  height: 100px;
  background: url(~static/logo.png);
}
</style>

