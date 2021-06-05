<template>
  <div class="flex justify-between p-4">
    <h1>Navbar</h1>
    <NuxtLink to="/">
      Articles List
    </NuxtLink>
    <p v-if="$strapi.user">
      Logged in
    </p>
  </div>
</template>
