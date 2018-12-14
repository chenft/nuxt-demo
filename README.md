# nuxt-demo

> Nuxt.js project

## Build Setup

```bash
# install dependencies
$ npm install # Or yarn install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, checkout the [Nuxt.js docs](https://github.com/nuxt/nuxt.js).

## Nuxt 常用配置项

### 配置 IP 和端口

```json
## package.json
config {
  nuxt: {
    host: '127.0.0.1',
    port: '7777'
  }
}
```

### 全局 css

```js
## nuxt.config.js
module.exports = {
  css: ['~assets/css/normalize.css']
}
```

### <nuxt-link> 标签

```html
<div>
  <ul>
    <li>
      <nuxt-link :to="{name:'index'}">home</nuxt-link>
      <nuxt-link :to="{name:'about'}">about</nuxt-link>
      <nuxt-link :to="{name:'news'}">news</nuxt-link>
    </li>
  </ul>
</div>
```

### params 传递参数

```html
<nuxt-link :to="{name:'news', params:{newsId:3306}}">news</nuxt-link>
```

```html
<div>
  <h2>news index page</h2>
  <p>newsId: {{ $route.params.newsId }}</p>
  <ul>
    <li><a href="/">home</a></li>
  </ul>
</div>
```

## Nuxt 的动态路由和参数校验

```html
## _id.vue ## _xx.vue, xx 和 $route.params[xx] 的 key 一致
<template>
  <div>
    <h2>news-content: [{{ $route.params.id }}]</h2>
    <ul>
      <li><a href="/">home</a></li>
    </ul>
  </div>
</template>
```

```html
<ul>
  <li><a href="/">home</a></li>
  <li><a href="/news/123">news-1</a></li>
  <li><a href="/news/456">news-2</a></li>
</ul>
```

### 动态参数校验

```js
<script>
## 校验不通过会进入 404 页面
export default {
  validate({ params }) {
    return /^\d+$/.test(params.id);
  }
};
</script>
```

## Nuxt 的路由动画效果

### 全局路由动画

```css
.page-enter-active,
.page-leave-active {
  transition: opacity 2s;
}
.page-enter,
.page-leave-active {
  opacity: 0;
}
```

```html
<ul>
  <li><nuxt-link :to="{name:'index'}">home</nuxt-link></li>
  <li>
    <!-- <a href="/news/123">news-1</a> -->
    <nuxt-link :to="{name:'news-id', params:{id:123}}">123</nuxt-link>
  </li>
  <li>
    <!-- <a href="/news/456">news-2</a> -->
    <nuxt-link :to="{name:'news-id', params:{id:456}}">456</nuxt-link>
  </li>
</ul>
```

### 单独设置页面动效

```css
.test-enter-active,
.test-leave-active {
  transition: all 2s;
  font-size: 12px;
}
.test-enter,
.test-leave-active {
  opacity: 0;
  font-size: 40px;
}
```

```js
export default {
  transition: 'test'
};
```

## Nuxt 的默认模版和默认布局

### 默认模板

```html
## app.html <!DOCTYPE html>
<html lang="en">
  ## 引用 nuxt.config.js 里的 head 配置
  <head>
    {{ HEAD }}
  </head>
  <body>
    fanty.top
    <div>{{ APP }}</div>
    ## 引用配置下的文件
  </body>
</html>
```

### 默认布局

```html
## layouts/default.vue
<template>
  <div>
    <p>lalala</p>
    <nuxt/>
  </div>
</template>
```

模版可以订制很多头部信息，包括 IE 版本的判断；模版只能定制<template>里的内容，跟布局有关系

## Nuxt 的错误页面和个性 meta 设置

### 错误页面

```html
## layouts/error.vue
```

```html
<template>
  <div>
    <h2 v-if="error.statusCode===404">404页面不存在</h2>
    <h2 v-else>500服务器错误</h2>
    <ul>
      <li><nuxt-link to="/">home</nuxt-link></li>
    </ul>
  </div>
</template>
```

```js
export default {
  props: ['error']
};
```

### 个性 meta 设置

```html
<ul>
  <li><nuxt-link :to="{name:'index'}">home</nuxt-link></li>
  <li>
    <nuxt-link :to="{name:'news-id', params:{id:123, title: 'aaaaaaaa'}}"
      >123</nuxt-link
    >
  </li>
  <li>
    <nuxt-link :to="{name:'news-id', params:{id:456, title:'bbbbbbbbbb'}}"
      >456</nuxt-link
    >
  </li>
</ul>
```

```html

```

```js
export default {
  data() {
    return {
      title: this.$route.params.title
    };
  },
  head() {
    return {
      title: this.title,
      meta: [
        {
          ## hid：唯一的标识编号，设置相同的 hid 可以覆盖 nuxt.config.js 里的配置
          hid: 'description',
          name: 'news',
          content: 'ccccc'
        }
      ]
    };
  }
};
```

## asyncData 方法获取数据

### ansycData 的 promise 方法

```js
export default {
  data() {
    return {
      name: 'hello world'
    };
  },
  async asyncData() {
    return axios.get('https://api.myjson.com/bins/1cjkuk').then(res => {
      console.log(res);
      return {
        info: res.data
      };
    });
  }
};
```

### ansycData 的 await 方法

```js
export default {
  data() {
    return {
      name: 'hello world'
    };
  },
  async asyncData() {
    let { data } = await axios.get('https://api.myjson.com/bins/1cjkuk');
    ## 自动设置 this.info = data
    return { info: data };
  }
};
```

## 静态资源和打包

### 直接引入图片

```html
<img src="~static/logo.png" alt />
```

### css 引入图片

```css
.diss {
  width: 300px;
  height: 100px;
  background: url(~static/logo.png);
}
```

### 打包静态 HTML 并运行

```bash
npm run generate
```

```bash
## cd dist
live-server
```
