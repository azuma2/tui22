
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
    <button @click="deleteContact(post.id)">削除</button>
    <p v-for="post in contactLists" :key="post">{{ post.content }}</p>


    
    <NuxtLink to="/logout">ログアウト</NuxtLink>
    <NuxtLink to="/component">コンポーネント</NuxtLink>
    <NuxtLink to="/comment">投稿</NuxtLink>
    <NuxtLink to="/login">ログイン</NuxtLink>
    <NuxtLink to="/register">登録</NuxtLink>
    <NuxtLink to="/comment">投稿</NuxtLink>
  </div>

        <table>
        <tr>
          <th>ID</th>
          <th>NAME</th>
          <th>EMAIL</th>
          <th>UPDATE</th>
          <th>DELETE</th>
        </tr>
        <tr >
          <td><p v-for="post in contactLists" :key="post">{{ post.content }}</p></td>
          <td></td>
          <td></td>
          <td>
            
              更新

          </td>
          <td>
            <button @click="deleteContact(post.id)">削除</button>
          </td>
        </tr>
      </table>
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

     async deleteContact(id) {
      await this.$axios.delete("http://127.0.0.1:8000/api/post/destroy/{id}" + id);
      this.getContact();
    },
    
    
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
