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
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
.diss {
  width: 300px;
  height: 100px;
  background: url(~static/logo.png);
}
</style>

