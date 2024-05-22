<template>
  <div class="pause-menu">
    <h1>Пауза</h1>
    <button @click="resumeGame">Продолжить</button>
    <button @click="restartGame">Перезапустить</button>
    <button @click="exitToMenu">Выйти в меню</button>
  </div>
</template>

<script setup lang="ts">
import { useRouter } from 'vue-router';

const router = useRouter();

const resumeGame = () => {
  alert('Что ты думал, в сказку попал? АХАХАХАХА плаки-плаки, начинай заново');
};

const restartGame = () => {
  router.push('/game');
};

const exitToMenu = () => {
  router.push('/');
};
</script>

<style lang="css" scoped>
.pause-menu {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  width : 30vw;
  background-color: rgba(0, 0, 0, 0.7);
  color: white;
 /* Добавленный отступ между кнопками и нижней частью меню */
}

.pause-menu button {
  display: inline-block;
  padding: 10px 20px;
  font-size: 24px;
  font-weight: bold;
  text-align: center;
  text-decoration: none;
  color: #fff;
  background-color: #ff5252;
  border: 2px solid #000;
  border-radius: 10px;
  box-shadow: 5px 5px 0px #000;
  transition: all 0.3s ease;
  cursor: pointer;
  margin-bottom: 1em; /* Добавленный отступ между кнопками */
}

.pause-menu button:hover {
  background-color: #fff;
  color: #ff5252;
  border: 2px solid #ff5252;
  box-shadow: 5px 5px 0px #ff5252;
}

.pause-menu button:active {
  background-color: #fcf414;
  box-shadow: none;
  transform: translateY(4px);
}
</style>
