<template>
  <div class="menu">
    <div class="header"></div>
    <div class="buttons">
      <router-link to="/game">
        <game-button class="btns"> Играть </game-button>
      </router-link>
      <div v-if="isAuth">
        <router-link to="/profile">
          <game-button class="btns"> Профиль </game-button>
        </router-link>
      </div>
      <div v-if="isAuth">
        <router-link to="/leaderboard">
          <game-button class="btns"> Лидерборд </game-button>
        </router-link>
      </div>
      <div v-if="!isAuth">
        <router-link to="/login">
          <game-button class="btns"> Войти </game-button>
        </router-link>
      </div>
    </div>
    <div v-if="isAuth">
      <div class="exit">
        <router-link to="/login">
          <game-button class="btns" @click="handleExit"> Выйти </game-button>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import GameButton from "../components/GameButton.vue";
export default defineComponent({
  components: {
    GameButton,
  },
  data() {
    let isAuth: Boolean = false;
    return {
      isAuth,
    };
  },
  async mounted() {
    this.checkAuth();
  },

  methods: {
    async handleExit() {
      localStorage.removeItem("token");
    },
    async checkAuth() {
      if (localStorage.getItem("token")) this.isAuth = true;
    },
  },
});
</script>

<style lang="css" scoped>
.menu {
  display: flex;
  flex-direction: column;
  margin-top: 20%;
}

.buttons {
  display: flex;
  flex-direction: column;
}

.btns {
  width: 10em;
  font-size: 4cqmin;
  margin-bottom: 0.5em;
}

.exit {
  align-self: center;
  margin-bottom: 2em;
}
</style>
