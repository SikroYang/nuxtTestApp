<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">{{forumName}}</h1>
    </div>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";
import axios from "axios";
export default {
  components: {
    Logo
  },
  head() {
    return {
      title: "个人详情"
    };
  },
  async asyncData({ params, redirect }) {
    if (!/^\d+$/.test(params.id)) return redirect("/404.html");
    let { data } = await axios.post(
      `http://www.iduilv.com/Api/ProjectLog/Detail/`,
      { id: params.id }
    );
    return { forumName: data.Data.title };
  }
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 50px;
  color: #35495e;
  letter-spacing: 1px;
}
</style>
