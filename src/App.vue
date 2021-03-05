<template>
  <v-app>
    <router-view></router-view>
  </v-app>
</template>

<script></script>
<style>
/* 解决页面左右溢出 */
html,
body {
  max-width: 100%;
  overflow-x: hidden;
  overflow-y: auto;
}
</style>
