<template>
  <NavBar />
  <router-view />

  <!-- footer -->
  <div class="text-light text-center p-3 bg-primary">
    Made with ❤ by 
    <a class="text-light" href="https://github.com/lutfialdrii">Lutfi Aldri Permana</a>
  </div>
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
