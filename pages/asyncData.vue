<template>
  <div>
    <h1>姓名：{{ info.name }}</h1>
    <h1>年龄：{{ info.age }}</h1>
    <h1>兴趣：{{ info.interest }}</h1>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data() {
    return {
      name: "hello world"
    };
  },
  async asyncData() {
    let { data } = await axios.get("https://api.myjson.com/bins/1cjkuk");
    return { info: data };
  }
};
</script>
