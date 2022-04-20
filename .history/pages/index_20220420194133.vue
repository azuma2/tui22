
<style>



p{
  color: #ffffff;
}

div{
  color: #ffffff;
}

.waku{
justify-content: space-between;
  display: flex;
}

.main2{

  display: block;
}
</style>

<template>
<div class="waku">
  <div class="tes">
  <FooSidebar></FooSidebar>
  </div>
  <div class="main2">
    <Nuxt />
    <NuxtLink to="/logout">ログアウト</NuxtLink>
    <NuxtLink to="/component">コンポーネント</NuxtLink>
    <NuxtLink to="/toukou">投稿</NuxtLink>
    <NuxtLink to="/login">ログイン</NuxtLink>
    <NuxtLink to="/register">登録</NuxtLink>
    <NuxtLink to="/come">投稿</NuxtLink>
  </div>
</div>
  
</template>

<script>
const body = {
  user_id: 1,
  content: '投稿内容',
};
const response = await this.$axios.post("http://127.0.0.1:8000/api/post/store", body);
console.log(response); // データの確認

</script>
