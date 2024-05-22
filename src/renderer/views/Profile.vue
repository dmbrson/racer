<template>
  <div>
    <div class="header">
      <h1>Профиль пользователя</h1>
      <div class="profile">
        <p>Имя: {{ user.username }}</p>
        <p>Email: {{ user.email }}</p>
        <p>Ваш рекорд: {{ user.score }}</p>
      </div>
    </div>
    <router-link to="/">
      <div class="exit">
        <game-button> Назад </game-button>
      </div>
    </router-link>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import GameButton from "../components/GameButton.vue";
import http from "../http_common";
import User from "../typings/User";

export default defineComponent({
  components: {
    GameButton,
  },
  data() {
    return {
      user: {} as User,
    };
  },
  async mounted() {
    try {
      const token = localStorage.getItem("token");
      if (token) {
        const response = await http.get("/profile/", {
          headers: {
            Authorization: `Token ${token}`,
          },
        });
        this.user = response.data;
        console.log(response);
      } else {
        console.log("No token found");
      }
    } catch (e) {
      console.error(e);
    }
  },
});
</script>

<style lang="css" scoped>
.header {
  color: #2f1e1e;
  margin-top: 7%;
  font-size: 30px;
  padding-left: 3%;
  width: 100%;
}
.profile {
  display: flex;
  flex-direction: column;
  width: 100%;
  background-color: #dbd9db;
  color: #2f1e1e;
  font-size: 22px;
  padding-left: 3%;
}

.exit {
  display: flex;
  position: absolute;
  justify-content: flex-end;
  width: 40%;
  bottom: 2em;
  right: 2em;
}
</style>
