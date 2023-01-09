<script setup>
import FormProfile from "./FormProfile.vue";
</script>

<script>
export default {
  data() {
    return { picture: "/src/assets/img/hero-image.jpg" };
  },
  methods: {
    getPicture(event) {
      this.picture = event;
    },
  },
};
</script>

<template>
  <section class="section-left">
    <FormProfile @get-picture="getPicture" />
  </section>
  <section class="section-right">
    <figure class="arrow arrow-back">
      <img src="../assets/img/back-arrow.svg" alt="back-arrow" />
    </figure>
    <figure class="picture">
      <img :src="picture" alt="profile-picture" />
    </figure>
    <figure class="arrow arrow-front">
      <img src="../assets/img/front-arrow.svg" alt="front-arrow" />
    </figure>
  </section>
</template>

<style scoped></style>
