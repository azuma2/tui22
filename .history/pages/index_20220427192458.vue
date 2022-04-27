
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
    <button @click="deleteContact(item.id)">削除</button>
    <p v-for="post in contactLists" :key="post">{{ post.content }}</p>

    
    
    <NuxtLink to="/logout">ログアウト</NuxtLink>
    <NuxtLink to="/component">コンポーネント</NuxtLink>
    <NuxtLink to="/comment">投稿</NuxtLink>
    <NuxtLink to="/login">ログイン</NuxtLink>
    <NuxtLink to="/register">登録</NuxtLink>
    <NuxtLink to="/comment">投稿</NuxtLink>
  </div>
</div>
  
  <div id="app">
    <h1>連絡先アプリ</h1>
    <div class="new">
      <h2>新規作成</h2>
      <div class="name">
        <label for="name">お名前：</label>
        <input type="text" name="name" id="name" v-model="newName" />
      </div>
      <div class="email">
        <label for="email">メールアドレス：</label>
        <input type="email" name="email" id="email" v-model="newEmail" />
      </div>
      <button @click="insertContact">新規作成</button>
    </div>
    <div class="table">
      <h2>連絡先リスト</h2>
      <table>
        <tr>
          <th>ID</th>
          <th>NAME</th>
          <th>EMAIL</th>
          <th>UPDATE</th>
          <th>DELETE</th>
        </tr>
        <tr v-for="item in contactLists" :key="item.id">
          <td>{{ item.id }}</td>
          <td><input type="text" v-model="item.name" /></td>
          <td><input type="email" v-model="item.email" /></td>
          <td>
            <button @click="updateContact(item.id, item.name, item.email)">
              更新
            </button>
          </td>
          <td>
            <button @click="deleteContact(item.id)">削除</button>
          </td>
        </tr>
      </table>
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
