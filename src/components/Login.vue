<template>
  <div>
      <h1>offco</h1>
      <h2>로그인 유지<input type="checkbox"></h2>
        <input class="form" type="text" placeholder="아이디" v-model="user.id"><br>
        <input class="form" type="password" placeholder="비밀번호" v-model="user.pw" @keyup.enter="login()"><br>
        <button class="bt_login_form" v-on:click="login" type="submit" >LOGIN</button><br>
    <h3><router-link to="/findid">아이디 찾기</router-link>&nbsp;&nbsp;&nbsp; | <router-link to="/findpw">&nbsp;&nbsp;&nbsp;비밀번호 찾기</router-link></h3>
    <button class="bt_signup_form" v-on:click="signup">회원가입</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    data: function() {
        return{
            user: {
                id: '',
                pw: ''
            }
        }
    },
    methods: {
        login: function() {
            
      // event.preventDefault(); //새로고침 방지
        console.log(this.user.id, this.user.pw);
        var url = 'https://jsonplaceholder.typicode.com/users';
        var data = {
            username: this.user.id,
            password: this.user.pw
         }
         console.log(data)
        axios.post(url, data).then((response)=> {
            if(response.data.success == true){
                console.log(response);
                this.$router.push('./');
            } else {
                alert("error")
            }
        }) 
        .catch(function(error) {
          console.log(error);
        })
        },
        signup: function() {
            this.$router.replace('./signup')
        },
        submitForm: function() {
      // event.preventDefault(); //새로고침 방지
      console.log(this.username, this.password);
      var url = 'https://jsonplaceholder.typicode.com/users';
      var data = {
        username: this.userid,
        password: this.userpw
      }
      axios.post(url, data)
        .then(function(response){
          console.log(response);
        }) 
        .catch(function(error) {
          console.log(error);
        })
    }
    }

}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Kite+One&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Gothic+A1&display=swap');
div {
    font-size: 10px;
    background-color: rgb(254, 249, 239);
    text-align: center;
    width : 100vw;
    height : 100vh;
}

h1 {
    display: inline-block;
    font-family: 'Kite One', sans-serif;
    font-weight: lighter;
    color: rgb(255, 134, 94);
    font-size: 9em;
    width: 62.5vw;
    height: 22.8vh;
    margin-top: 0.45em;
    margin-bottom: 0;
  }
  h2 {
      margin-left: auto;
      margin-right: 2em;
      font-weight: lighter;
      font-family: 'Gothic A1', sans-serif;
      font-size: 1.3em;
      width: 28.1vw;
      height: 2.63vh;
      margin-top: 2.31em;
  }
  .form {
      display: inline-block;
      width: 82vw;
      height: 6.1vh;
      margin-left: 0;
      margin-bottom: 1.15em;
      border:1px solid rgba(162, 210, 255, 100);
      border-radius: 15px;
  }
  .bt_login_form {
      font-family: 'Gothic A1', sans-serif;
      font-size: 2.6em;
      width: 82vw;
      height: 9vh;
      border: rgb(28, 31, 34);
      border-radius: 15px;
      background-color: rgb(162, 210, 255);
      color: rgb(57, 62, 70);
      margin-top: 0.8em;
      margin-bottom: 0.8em;

  }
  .bt_signup_form {
      font-family: 'Gothic A1', sans-serif;
      font-size: 2.6em;
      width: 82vw;
      height: 9vh;
      border:1px solid rgb(255, 134, 94);
      border-radius: 15px;
      background-color: white;
      color: rgb(255, 134, 94);
      margin-top: 0.8em;
  }
  a {
      text-decoration: none;
      color: rgb(57, 62, 70);
      margin-top: 0;

  }
  h3 {
      margin-top: 0;
      margin-bottom: 0;
      font-weight:normal;
  }
</style>