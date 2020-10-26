<template>
  <div>
    <transition name="fade">
      <div class="preloader" v-if="loading">
        <svg viewBox="0 0 32 32" width="48" height="48">
          <use href="@/assets/img/sahkyo.svg#sahkyo" />
        </svg>
      </div>
    </transition>
    <main :class="currentPage">
      <the-header />
      <Nuxt />
    </main>
  </div>
</template>

<script>
import imagesLoaded from "imagesloaded";
import TheHeader from "@/components/TheHeader";
export default {
  data() {
    return {
      loading: true,
    };
  },
  mounted() {
    var images = document.querySelectorAll("img");
    imagesLoaded(images, () => (this.loading = false));
  },
  components: {
    TheHeader,
  },
  computed: {
    currentPage() {
      return this.$route.name;
    },
  },
};
</script>
