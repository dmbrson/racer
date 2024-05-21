<script setup lang="ts"></script>

<template>
  <router-view> </router-view>
</template>

<style lang="css">
@import url("https://fonts.googleapis.com/css2?family=Comfortaa:wght@300;400;500&display=swap");

body {
  margin: 0;
  padding: 0;
  font-family: "Comfortaa", sans-serif;
  background: conic-gradient(
      from 45deg at 75% 75%,
      var(--c3) 90deg,
      var(--c1) 0 180deg,
      #0000 0
    ),
    conic-gradient(from -45deg at 25% 25%, var(--c3) 90deg, #0000 0),
    conic-gradient(from -45deg at 50% 100%, #0000 180deg, var(--c3) 0),
    conic-gradient(
      from -45deg,
      var(--c1) 90deg,
      var(--c2) 0 225deg,
      var(--c4) 0
    );
  background-size: var(--s) var(--s);
  --s: 150px; /* control the size */
  --c1: #ff847c;
  --c2: #e84a5f;
  --c3: #fecea8;
  --c4: #99b898;
  color: #7f9e9f;
  color: #7f9e9f;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
