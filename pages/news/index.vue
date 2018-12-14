<template>
  <div>
    <h2>news index page</h2>
    <p>newsId: {{ $route.params.newsId }}</p>
    <ul>
      <li>
        <nuxt-link :to="{name:'index'}">home</nuxt-link>
      </li>
      <li>
        <!-- <a href="/news/123">news-1</a> -->
        <nuxt-link :to="{name:'news-id', params:{id:123, title: 'aaaaaaaa'}}">123</nuxt-link>
      </li>
      <li>
        <!-- <a href="/news/456">news-2</a> -->
        <nuxt-link :to="{name:'news-id', params:{id:456, title:'bbbbbbbbbb'}}">456</nuxt-link>
      </li>
    </ul>
  </div>
</template>
