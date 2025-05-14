<!-- u18135600 Daniel Stevens -->

<template>
  <div id="app">
    <nav>
      <ul>
        <li><NuxtLink to="/">Home</NuxtLink></li>
        <li><NuxtLink to="/search">Search</NuxtLink></li>
      </ul>
    </nav>
    <NuxtPage/>    
  </div>

</template>

<style scoped>
body{
  margin: 0;
}
#app {
  background-color: #0b1f20;
  min-height: 100vh;
  font-family: Arial, sans-serif;
  color: #a1a1a1;
  margin: 0;
}

nav {
  background-color: #123335;
  padding: 1rem;
}

nav ul {
  display: flex;
  list-style: none;
  gap: 1.5rem;
  margin: 0;
  padding: 0;
}

nav a {
  color: #19bff2;
  font-weight: bold;
  text-decoration: none;
}

nav a:hover {
  text-decoration: underline;
}
</style>

<style>
body {
  margin: 0;
  padding: 0;
  background-color: #0e1e17;
}
</style>