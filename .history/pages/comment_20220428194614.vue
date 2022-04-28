
<style >
h2{
   text-align: left;
   padding: 5px;
}
</style>

<template>
<div class="waku">
  <div class="tes">
  <FooSidebar @updateContent="updateContent"></FooSidebar>
  <Register @updateName="updateName"></Register>
  </div>
  <div class="main2">


    


        <table class=oowaku>
        <tr>
          <th><h1>ホーム</h1> </th>

        </tr>
        <tr >
          <td class=post>
            <div class=post2  v-for="post in contactLists" :key="post">
            名前{{ post.user.name }}
            
              <button class="btn3" @click="deleteContact(post.id)"><img class="icon" src="/img/heart.png"></button>
              <button class="btn4" @click="deleteContact(post.id)"><img class="icon" src="/img/cross.png"></button>
          
            
            
            <br>
            <p class=post3>{{ post.content }}</p>
            </div>
            
            </td>
            <td>
              <h2>コメント</h2>
            </td>
            <td>

            </td>
            

        </tr>
      </table>
      <h2>コメント</h2>
      <p>{{ message }}</p>
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
      user: "",
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
    updateName(name) {
      this.name = name;
 
    },
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

      console.log(sendData)

      await this.$axios.post("http://127.0.0.1:8000/api/post/store", sendData).then( res => {
          location.reload();
          })
      this.content = "";
      this.getContact();
      
      console.log(sendData);
      location.reload();


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



<style>



</style>