<template>
  <div>
    <!-- setup中return了在这里就可以直接调用了{{。。。}}两个大括号调用-->
    <div>Bot昵称：{{ bot_name }}</div>  
    <div>Bot战力：{{ bot_rating }}</div>
  </div>
  <router-view/>
</template>

<script>
import $ from 'jquery';
import { ref } from 'vue';  //定义两个变量：昵称和战力。vue里定义变量需要ref

export default {
  name: "App",
  setup: () => {  //setup是整个函数的入口
    let bot_name = ref("");
    let bot_rating = ref("");

    //访问后端连接，可以用ajax写
    $.ajax({
      url: "http://127.0.0.1:3000/pk/getbotinfo/",  //url是我们的函数地址
      type: "get",  //请求就两种get获取数据，post是创建数据
      success: resp => {
        bot_name.value = resp.name;
        bot_rating.value = resp.rating;
      }
    });

    return {
      bot_name,
      bot_rating
    }
  }
}
</script>

<style>
body {
  background-image: url("@/assets/background.png");
  background-size: cover;   /* //100%填充图片 */
}
</style>