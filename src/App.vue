<template>
  <link rel="stylesheet" href="https://unpkg.com/@picocss/pico@latest/css/pico.min.css">
  <nav class="container-fluid">
    <ul>
      <li><router-link to="/">Home</router-link></li>
      <li><router-link to="/wordle">wordle</router-link></li>
    </ul>
  </nav>
  <main class="container">
    <router-view/>
  </main>
</template>