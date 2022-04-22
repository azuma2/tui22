
<template>
<div class="row">
<div class="col-3">
  <div class="sidebar">
    <div class="sidebar-wrapper">
      <div class="sidebar-link-area">
        <div class="logo2"><img class="logo" src="/img/logo.png"></div>
        <!-- サイドバーメニュー -->
        <div class="syde">
          
          <div class="icon2"><img class="icon" src="/img/home.png"></div><NuxtLink to="/"><p class="moji">ホーム</p></NuxtLink>
        </div>
        <div class="syde">
          <div class="icon2"><img class="icon" src="/img/logout.png"></div><NuxtLink to="/logout"><p class="moji">ログアウト</p></NuxtLink>
        </div>
        <p class="moji">シェア</p>


        
          <textarea class="area" type="text"  name="post" />
          <div class="btnichi">
            <input class="btn2" type="submit" @click="insertContact"  v-model="post" value="シェアする" />
          </div>
        

      </div>
    </div>
  </div>
  </div>
</div>
</template>




<script>

export default {
  data() {
    return {
      user_id: "",
      content: "",
      contactLists: [],
    };
  },
  methods: {
    async getContact() {
      const resData = await this.$axios.get(
        "http://127.0.0.1:8000/api/post/store"
      );
      this.contactLists = resData.data.data;
      console.log(response);
    },
    async insertContact() {
      const sendData = {
        user_id: this.newUser_id,
        content: this.newContent,
      };
      await this.$axios.post("http://127.0.0.1:8000/api/post/store", sendData);
      this.getContact();
      console.log(response);
    },
  },
  created() {
    this.getContact();
  },
};

</script>