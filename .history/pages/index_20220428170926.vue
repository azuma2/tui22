
<style>


    body {
      font-size:16px;
      margin: 5px;
  background-color: rgb(41, 45, 88);
    }
    
    .oowaku{
    width: 2000px;
    margin-right:-1800px;
    }

.narabe{
  text-align: center;
}
    
        td {
      
      text-align: center;
    }

    .narabe{
        flex-flow: column;
    }


div{
  color: #ffffff;
}

h1{
   text-align: left;
   padding: 5px;
}

.post{
  text-align: left;
  border: solid;border-color: #fff;
  border-width: 1px;
}

.post2{
  border: solid;border-color: #fff;
  border-width: 1px;
  padding: 20px;
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
cursor: pointer;
margin-right: 30px;
ma: 5px;
}

.btn4{
background-color: transparent;
cursor: pointer;
}

.btn5{
background-color: transparent;
cursor: pointer;
}


</style>

<template>
<div class="waku">
  <div class="tes">
  <FooSidebar @updateContent="updateContent"></FooSidebar>
  <Register @updateName="updateName"></Register>
  </div>
  <div class="main2">

    <NuxtLink to="/logout">ログアウト</NuxtLink>
    <NuxtLink to="/login">ログイン</NuxtLink>
    <NuxtLink to="/register">登録</NuxtLink>
    


        <table class=oowaku>
        <tr>
          <th><h1>ホーム</h1></th>

        </tr>
        <tr >
          <td class=post>
            <div class=post2  v-for="post in contactLists" :key="post">
            名前{{ user.name }}
            
              <button class="btn3" @click="deleteContact(post.id)"><img class="icon" src="/img/heart.png"></button>
              <button class="btn4" @click="deleteContact(post.id)"><img class="icon" src="/img/cross.png"></button>
          
              <NuxtLink to="/comment"><button class="btn5"><img class="icon" src="/img/feather.png"></button></NuxtLink>
            
            <br>
            {{ post.content }}
            </div></td>
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
      user: "",
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
    updateName(name) {
      this.name = name;
 
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
