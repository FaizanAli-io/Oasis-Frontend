<template>
  <main>
    <h1> Why hello there, would you like some... </h1>
    <RouterLink :to="{ name: 'admin' }" class="text-xl text-green-500">
      Admin Privelages?
    </RouterLink>
  </main>
</template>
