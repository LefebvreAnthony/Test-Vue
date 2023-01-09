<script>
import axios from "axios";

export default {
  props: {
    method: { type: Function },
  },
  data() {
    return {
      person: "",
      profiles: [],
      picture: "",
      url: "/src/assets/img/hero-image.jpg",
    };
  },
  methods: {
    changePicture(url) {
      this.url = url;
      this.$emit("get-picture", this.url);
    },
    addInfos(event) {
      this.picture = event.target.selectedOptions[0].getAttribute("url");
      this.person = event.target.value;
    },
  },
  mounted() {
    try {
      axios
        .get("https://randomuser.me/api/?results=50&inc=name,picture")
        .then((response) => {
          this.person = `${
            response.data.results[0].name.first
          } ${response.data.results[0].name.last.charAt(0)}`;
          this.profiles = response.data.results;
        });
    } catch (err) {
      console.log(err);
    }
  },
};
</script>

<template>
  <h1>
    Bonjour<br /><span class="name">{{ person }}.</span>
  </h1>
  <form v-on:submit.prevent="onSubmit">
    <div>
      <label>Selectionner un nouveau profil à l'aide de cette liste : </label>
      <select name="profile" id="profile" @change="addInfos($event)">
        <option
          v-for="(profile, index) in profiles"
          v-bind:key="index"
          data-img="{{
          profile.picture.medium
          }}"
          v-bind="{ id: index, url: profile.picture.large }"
          :value="`${profile.name.first} ${profile.name.last.charAt(0)}`"
        >
          {{ profile.name.first }} {{ profile.name.last }}
        </option>
      </select>
    </div>
    <button @click="changePicture(picture)">Afficher sa photo de profil</button>
  </form>
</template>

<style scoped>
h1 {
  font-size: 3em;
  font-weight: bold;
  color: rgb(57, 56, 56);
}
form {
  font-size: 1.1em;
}
form div {
  margin: 2em 0;
}
button {
  color: #fff;
  background-color: #000;
  text-transform: uppercase;
  padding: 1em 2em;
  border: none;
  border-radius: 25px;
}
.name {
  text-transform: uppercase;
}
select {
  font-weight: 600;
}
</style>
