<template>
  <!-- <audio controls src="Alafasy/mp3/002001.mp3">
    Your browser does not support the
    <code>audio</code> element.
  </audio> -->
  <NavBar />
  <router-view />
</template>

<script>
import { ref } from "vue";
import axios from "axios";
import NavBar from "../../uts/src/components/NavBar.vue";

export default {
  components: {
    NavBar,
  },
};
</script>
