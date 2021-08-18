<template>
  <div class="flex">
    <!-- <pre> {{ $data }}</pre> -->
    <h1 class="title">Nuxt Galaxy</h1>
    <p v-if="$fetchState.pending">Fetching planets...</p>
    <p v-if="$fetchState.error">Error while fecthing...</p>
    <ul>
      <li v-for="planet in planets" :key="planet.slug">
        <NuxtLink :to="planet.slug">{{ planet.title }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  layout: 'home',
  async fetch() {
    this.planets = await fetch('https://api.nuxtjs.dev/planets').then((res) => {
      if (res.ok) {
        return res.json()
      }
      throw new Error(res.status)
    })
  },
  data() {
    return {
      planets: [],
    }
  },
}
</script>
