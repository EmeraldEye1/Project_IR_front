<template>
  <!-- component -->
  <div class="body1">
    <h1 class="body1">Anime Star Battle</h1>
    <div class="">
      <div class=""></div>
      <div class="">
        <div class="">
          <div class="body2"></div>
          <div class="body2">
            <div class="page2">
              <img class="img" src="@/assets/Dmslay.jpg" alt="Paris" />
            </div>
            <div class="body2">
              <div class="">
                <Form @submit="handleLogin" :validation-schema="schema">
                  <div class="page">
                    <div class="input">
                      <Field
                        autocomplete="off"
                        id="username"
                        name="username"
                        type="text"
                        class=""
                        placeholder="username"
                      />
                      <ErrorMessage name="username" class="left" />
                      <label for="username" class="username">Username</label>
                    </div>
                    <div class="input">
                      <Field
                        autocomplete="off"
                        id="password"
                        name="password"
                        type="password"
                        class=""
                        placeholder="Password"
                      />
                      <ErrorMessage name="password" class="left" />
                      <label for="password" class="password">Password</label>
                    </div>
                    <div class="">
                      <button class="login :hover">Login</button>
                    </div>
                  </div>
                </Form>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { Form, Field, ErrorMessage } from 'vee-validate'
import * as yup from 'yup'
import AuthService from '@/service/AuthService.js'
export default {
  name: 'LoginView',
  components: {
    Form,
    Field,
    ErrorMessage
  },
  data() {
    const schema = yup.object().shape({
      username: yup.string().required('User name is required!'),
      password: yup.string().required('Password is required!')
    })
    return {
      loading: false,
      message: '',
      schema
    }
  },
  methods: {
    handleLogin(user) {
      AuthService.login(user)
        .then(() => {
          this.$router.push({ path: '/' })
        })
        .catch(() => {
          this.message = 'could not login'
        })
    }
  }
}
</script>
<style scoped>
@import url('https://rsms.me/inter/inter-ui.css');
::selection {
  background: #2d2f36;
}
::-webkit-selection {
  background: #2d2f36;
}
::-moz-selection {
  background: #2d2f36;
}
.body2 {
  background-image: url('@/assets/my.jpg');
  border: 5px solid red;
  box-sizing: border-box;
  margin: 0;
  padding: 100%;
  position: fixed;
  background-repeat: no-repeat;
  background-size: cover;
}
.body {
  background: rgb(112, 144, 213);
  font-family: 'Inter UI', sans-serif;
  margin: 0;
  padding: 20px;
}
.img {
  /* margin: 50px 40px 40px 370px; */
  width: 350px;
  height: 400px;
}
.page2 {
  /* margin: 50px 40px 40px 370px; */
  width: 350px;
  height: 200px;
  top: 20%;
  left: 66%;
  margin-left: -250px; /* Negative half of width. */
  /* display: flex; */
  flex-direction: column;
  position: fixed;
}
.page {
  /* margin: 50px 40px 40px 370px; */
  width: 500px;
  height: 200px;
  top: 20%;
  left: 40%;
  margin-left: -250px; /* Negative half of width. */
  background: #0e85c0;
  /* display: flex; */
  flex-direction: column;
  height: 400px;
  position: fixed;
  /* place-content: center; */
  width: 400px;
  border: solid 5px green;
  padding: 5px;
  display: inline-block;
}
/* @media (max-width: 767px) {
  .page {
    height: auto;
    margin-bottom: 20px;
    padding-bottom: 20px;
  }
} */
/* .container {
  display: flex;
  height: 320px;
  margin: 0 auto;
  width: 640px;
}
@media (max-width: 767px) {
  .container {
    flex-direction: column;
    height: 630px;
    width: 320px;
  }
} */
.left {
  font-size: 10px;
  font-weight: 10px;
  color: rgb(255, 0, 0);
  position: relative;
  width: 12%;
}
/* @media (max-width: 767px) {
  .left {
    height: 100%;
    left: 20px;
    width: calc(100% - 40px);
    max-height: 270px;
  } */
/* } */
.erorr-feedback {
  -ms-text-size-adjust: 10px;
}
.login {
  font-size: 25px;
  font-weight: 750;
  margin: 70px 40px 40px;
  background-color: pink;
}

.eula {
  color: #999;
  font-size: 14px;
  line-height: 1.5;
  margin: 40px;
}
.right {
  background: #474a59;
  box-shadow: 0px 0px 40px 16px rgba(0, 0, 0, 0.22);
  color: #f1f1f2;
  position: relative;
  width: 50%;
}
@media (max-width: 767px) {
  .right {
    flex-shrink: 0;
    height: 100%;
    width: 100%;
    max-height: 350px;
  }
}
svg {
  position: absolute;
  width: 320px;
}
path {
  fill: none;
  stroke: url(#linearGradient);
  stroke-width: 4;
  stroke-dasharray: 240 1386;
}
.form {
  margin: 40px;
  position: absolute;
}
label {
  color: #c2c2c5;
  display: block;
  font-size: 14px;
  height: 16px;
  margin-top: 20px;
  margin-bottom: 5px;
}
.username {
  margin: 0px 0px 300px;
}
.password {
  margin: 0px 0px 300px;
}
.input {
  margin: 50px 0px 0px;
  /* background: transparent; */
  border: 0;
  color: #f2f2f2;
  font-size: 20px;
  height: 30px;
  line-height: 30px;
  outline: none !important;
  width: 100%;
}
/* input::-moz-focus-inner {
  border: 0;
}
#submit {
  color: #707075;
  margin-top: 40px;
  transition: color 300ms;
}
#submit:focus {
  color: #f2f2f2;
}
#submit:active {
  color: #d0d0d2;
} */
</style>
