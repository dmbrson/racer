<template>
  <div class="login-form">
    <form @submit.prevent="login">
      <div class="form">
        <div class="wave-group">
          <input v-model="username" type="text" required class="input" />
          <span class="bar"></span>
          <label class="label">
            <span class="label-char" style="--index: 0">И</span>
            <span class="label-char" style="--index: 1">м</span>
            <span class="label-char" style="--index: 2">я</span>
            <span class="label-char" style="--index: 3">&nbsp;</span>
            <span class="label-char" style="--index: 4">П</span>
            <span class="label-char" style="--index: 4">о</span>
            <span class="label-char" style="--index: 4">л</span>
            <span class="label-char" style="--index: 4">ь</span>
            <span class="label-char" style="--index: 4">з</span>
            <span class="label-char" style="--index: 4">о</span>
            <span class="label-char" style="--index: 4">в</span>
            <span class="label-char" style="--index: 4">а</span>
            <span class="label-char" style="--index: 4">т</span>
            <span class="label-char" style="--index: 4">е</span>
            <span class="label-char" style="--index: 4">л</span>
            <span class="label-char" style="--index: 4">я</span>
          </label>
        </div>
        <div class="wave-group">
          <input
            v-model="password"
            required
            id="password"
            type="password"
            class="input"
          />
          <span class="bar"></span>
          <label class="label">
            <span class="label-char" style="--index: 0">П</span>
            <span class="label-char" style="--index: 1">а</span>
            <span class="label-char" style="--index: 2">р</span>
            <span class="label-char" style="--index: 3">о</span>
            <span class="label-char" style="--index: 4">л</span>
            <span class="label-char" style="--index: 5">ь</span>
          </label>
        </div>
        <div>
          <game-button type="submit" class="enter"> Войти </game-button>
        </div>
        <div>
          <router-link to="/register">
            <a class="reg">Регистрация</a>
          </router-link>
        </div>
      </div>
    </form>
  </div>
</template>

<script lang="ts">
import http from "../http_common";
import GameButton from "../components/GameButton.vue";

export default {
  components: {
    GameButton,
  },

  data() {
    return {
      username: "",
      password: "",
      isShow: false,
      isAuth: false,
    };
  },

  methods: {
    async login() {
      try {
        const response = await http.post("/login/", {
          username: this.username,
          password: this.password,
        });

        const token = response.data.token;

        if (token) {
          localStorage.setItem("token", token);
          this.isAuth = true;
          this.$router.push("/");
        }
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

<style scoped lang="css">
.wave-group {
  position: relative;
}
.wave-group .input {
  font-size: 16px;
  padding: 10px 10px 10px 5px;
  display: block;
  width: 200px;
  color: #dbd9db;
  border: none;
  border-bottom: 1px solid #515151;
  background: transparent;
}

.wave-group .input:focus {
  outline: none;
}

.wave-group .label {
  color: #999;
  font-size: 18px;
  font-weight: normal;
  position: absolute;
  pointer-events: none;
  left: 5px;
  top: 10px;
  display: flex;
}

.wave-group .label-char {
  transition: 0.2s ease all;
  transition-delay: calc(var(--index) * 0.05s);
}

.wave-group .input:focus ~ label .label-char,
.wave-group .input:valid ~ label .label-char {
  transform: translateY(-20px);
  font-size: 14px;
  color: #5264ae;
}

.wave-group .bar {
  position: relative;
  display: block;
  width: 200px;
}

.wave-group .bar:before,
.wave-group .bar:after {
  content: "";
  height: 2px;
  width: 0;
  bottom: 1px;
  position: absolute;
  background: #5264ae;
  transition: 0.2s ease all;
  -moz-transition: 0.2s ease all;
  -webkit-transition: 0.2s ease all;
}

.wave-group .bar:before {
  left: 50%;
}

.wave-group .bar:after {
  right: 50%;
}

.wave-group .input:focus ~ .bar:before,
.wave-group .input:focus ~ .bar:after {
  width: 50%;
}
.login-form {
  display: flex;
  flex-direction: column;
  margin-top: 20%;
  align-items: center;
  justify-content: center;
}

.form {
  display: flex;
  flex-direction: column;
  background-color: #2a2a3f;
  border-radius: 5px;
  padding: 45px;
  align-items: center;
}

.form input {
  margin-bottom: 10px;
}

.form div {
  margin-bottom: 10px;
}

input:focus {
  outline: none;
}
</style>
