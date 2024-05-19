<template>
  <div>
    <div>
      <h1>Профиль пользователя</h1>
      <p>Имя: {{ user.username }}</p>
      <p>Email: {{ user.email }}</p>
      <p>Ваш рекорд: {{ user.score }}</p>
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
.profile {
  display: flex;
  flex-direction: column;
  width: 35%;
  color: #2f1e1e;
  font-size: 22px;
}

.exit {
  display: flex;
  position: absolute;
  justify-content: center;
  width: 35%;
  bottom: 2em;
}

.avatar-photo {
  width: 35%;
  margin-left: 0.5em;
}

.profile-photo {
  display: flex;
  flex-direction: row;
}

.field {
  display: flex;
}

.profile-info {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  width: 65%;
  padding-left: 1em;
}

.copy-img {
  width: 100%;
}

#copy-id {
  width: 15%;
  margin-left: 1em;
  background: none;
  border: 3px solid #8496ae;
  border-radius: 10px;
  background: #8496ae;
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

#copy-id:hover {
  box-shadow: 0 12px 16px 0 rgba(0, 0, 0, 0.24),
    0 17px 50px 0 rgba(0, 0, 0, 0.19);
}

#copy-name {
  width: 15%;
  margin-left: 1em;
  background: none;
  border: 3px solid #8496ae;
  border-radius: 10px;
  background: #8496ae;
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

#copy-name:hover {
  box-shadow: 0 12px 16px 0 rgba(0, 0, 0, 0.24),
    0 17px 50px 0 rgba(0, 0, 0, 0.19);
}

#id {
  width: 70%;
  background-color: #657d7d;
  color: #dee7e3;
  padding: 0.5em;
  border-radius: 5px;
  font-size: 18px;
}

#name {
  width: 70%;
  background-color: #657d7d;
  color: #dee7e3;
  padding: 0.5em;
  border-radius: 5px;
  font-size: 18px;
}

.scores {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 0.5em;
}

.header {
  background-color: #060223;
  font-size: 30px;
  text-align: center;
  padding: 20px;
  color: #7f9e9f;
  font-weight: 700;
}

.main-info {
  border-radius: 10px;
  background-color: #b8cece;
  padding: 10px;
}
</style>
