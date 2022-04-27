
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
    <p>{{ message }}</p>
    
    <NuxtLink to="/logout">ログアウト</NuxtLink>
    <NuxtLink to="/component">コンポーネント</NuxtLink>
    <NuxtLink to="/toukou">投稿</NuxtLink>
    <NuxtLink to="/login">ログイン</NuxtLink>
    <NuxtLink to="/register">登録</NuxtLink>
    <NuxtLink to="/comment">投稿</NuxtLink>
  </div>
</div>
  
</template>

<script>

import firebase from '~/plugins/firebase'
export default {
  
  data() {
    
    return {
      message: 'ログインができておりません',
    }
  },
  created() {
 
    firebase.auth().onAuthStateChanged((user) => {
      if (user) {
        this.message = 'ログイン済みです'
      }
    })
  },
}

</script>
