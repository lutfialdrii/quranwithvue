<template>
  <div v-for="chapter in listSurah" :key="chapter.id" class="row">
    <div class="col-sm-6">
      <div class="card">
        <div class="card-body">
          <h5 class="card-title">{{ chapter.name_simple }}</h5>
          <p class="card-text">{{ chapter.translated_name.name }}</p>
          <a href="#" class="btn btn-primary">Baca</a>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { ref, watch } from "vue";
import axios from "axios";

export default {
  data() {
    return {
      nomor: "1",
      judul: "",
      arti: "",
      listSurah: ref([]),
      namaSurah: "",
    };
  },

  watch: {
    nomor() {
      this.getSurah();
    },
  },

  mounted() {
    this.getSurah();
    this.getlistSurah();
  },

  methods: {
    getSurah() {
      axios
        .get(`https://api.quran.com/api/v4/chapters/${this.nomor}?language=id`)
        .then((response) => {
          this.judul = response.data.chapter;
          this.arti = this.judul.translated_name;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getlistSurah() {
      axios
        .get(`https://api.quran.com/api/v4/chapters?language=id`)
        .then((response) => {
          this.listSurah = response.data.chapters;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
