
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
  <FooSidebar @updateContent="updateContent"></FooSidebar>
  </div>
  <div class="main2">
    <Nuxt />
    <p>{{ message }}</p>
    <p>{{ content }}</p>
    <p>{{ contactLists }}</p>
    
    
    <NuxtLink to="/logout">ログアウト</NuxtLink>
    <NuxtLink to="/component">コンポーネント</NuxtLink>
    <NuxtLink to="/comment">投稿</NuxtLink>
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


  methods: {
    
    
    async getContact() {
      const response = await this.$axios.get(
      "http://127.0.0.1:8000/api/posts"
      );
      this.contactLists = response.data.items;
      console.log(response);
    },
    


    updateContent(content) {
      this.content = content;
    },
  },

  created() {

    
    
 
    firebase.auth().onAuthStateChanged((user) => {
      if (user) {
        this.message = 'ログイン済みです'
      }
    })
    this.getContact()
  },
}

</script>
