
<style>





div{
  color: #ffffff;
}

h1{
   text-align: left;
}

.post{
  text-align: left;
}

    tr{
      border: solid;border-color: #fff;
      border-width: 1px;
    }

    table{
    border-collapse: collapse;
    }



.waku{
justify-content: space-between;
  display: flex;
    width: 650px;
    padding: 10px;
    position: absolute;
    top: 0px;
    left: 1%;
}

.main2{

  display: block;
}

.icon{
      height: 25px;
      width: 25px;
}

.btn3{
background-color: transparent;
}
</style>

<template>
<div class="waku">
  <div class="tes">
  <FooSidebar @updateContent="updateContent"></FooSidebar>
  </div>
  <div class="main2">

    <NuxtLink to="/logout">ログアウト</NuxtLink>
    <NuxtLink to="/login">ログイン</NuxtLink>
    <NuxtLink to="/register">登録</NuxtLink>
    <NuxtLink to="/comment">投稿</NuxtLink>


        <table>
        <tr>
          <th><h1>ホーム</h1></th>

        </tr>
        <tr >
          <td class=post><p v-for="post in contactLists" :key="post">
            名前
            <button class="btn3" @click="deleteContact(post.id)"><img class="icon" src="/img/heart.png"></button>
            <button class="btn3" @click="deleteContact(post.id)"><img class="icon" src="/img/cross.png"></button>
             
            <button class="btn3" @click="deleteContact(post.id)"><img class="icon" src="/img/feather.png"></button><br>
            {{ post.content }}
            </p></td>
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
      await this.$axios.delete("http://127.0.0.1:8000/api/post/destroy/" + id);
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
