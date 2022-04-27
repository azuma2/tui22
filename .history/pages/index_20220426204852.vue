
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
    <p>{{ content }}</p>
    
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
      user_id: "",
      content: "",
      contactLists: [],
      message: 'ログインができておりません',
    }
    
  },


      async insertContact() {
      　console.log(this.user_id)
    console.log(this.content)
      const sendData = {
        user_id: this.user_id,
        content: this.content,
        created_at: this.created_at,
        updated_at: this.updated_at,
      };
  created() {
 
    firebase.auth().onAuthStateChanged((user) => {
      if (user) {
        this.message = 'ログイン済みです'
      }
    })
  },
}

</script>
