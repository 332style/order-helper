<template>
  <el-container class="container">
    <el-main>
      <div class="user-form">
        <el-input v-model="email" placeholder="請輸入帳號"></el-input>
        <el-input v-model="password" placeholder="請輸入密碼" show-password />
        <el-button type="primary" @click="loginWithEmail">登入</el-button>
        <el-button type="success" @click="loginWithGoogle">
          <font-awesome-icon :icon="['fab', 'google']" />
        </el-button>
      </div>
    </el-main>
  </el-container>
</template>
<script>
import * as firebase from "firebase";

export default {
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    loginWithEmail() {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
        .catch(function(error) {
          // Handle Errors here.
          const errorCode = error.code;
          const errorMessage = error.message;
          console.log(errorCode, errorMessage);
          // ...
        });
    },
    loginWithGoogle() {
      const provider = new firebase.auth.GoogleAuthProvider();
      firebase
        .auth()
        .signInWithPopup(provider)
        .then(function(result) {
          // This gives you a Google Access Token. You can use it to access the Google API.
          // const token = result.credential.accessToken;
          // The signed-in user info.
          const user = result.user;
          console.log("user", user);
          // ...
        })
        .catch(function(error) {
          // Handle Errors here.
          const errorCode = error.code;
          const errorMessage = error.message;
          // The email of the user's account used.
          // const email = error.email;
          // The firebase.auth.AuthCredential type that was used.
          // const credential = error.credential;
          console.log(errorCode, errorMessage);
        });
    }
  }
};
</script>
<style lang="scss">
.container {
  main {
    display: flex;
    justify-content: center;
    .user-form {
      max-width: 350px;
      border: 1px solid rgba(0, 0, 0, 0.6);
      border-radius: 5px;
      padding: 20px;
      .el-input {
        margin: 10px 0;
      }
      .el-button {
        margin-top: 10px;
      }
    }
  }
}
</style>