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
    router.back();
  };
  
  const restartGame = () => {
    router.push('/game');
  };
  
  const exitToMenu = () => {
    router.push('/');
  };
  </script>
  
  <style scoped>
  .pause-menu {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.7);
    color: white;
  }
  
  .pause-menu button {
    margin: 10px;
    padding: 10px 20px;
    font-size: 18px;
    cursor: pointer;
  }
  </style>
  