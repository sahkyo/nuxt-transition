<template>
  <main :class="currentPage">
    <the-header />
    <Nuxt />
  </main>
</template>

<script>
import TheHeader from "@/components/TheHeader";
export default {
  components: {
    TheHeader
  },
  computed: {
    currentPage() {
      return this.$route.name
    }
  }
}
</script>
