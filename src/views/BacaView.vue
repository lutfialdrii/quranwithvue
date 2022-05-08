<template>
  <!-- list Surat -->
  <div class="dropdown">
    <a class="btn btn-secondary dropdown-toggle" href="#" role="button" id="dropdownMenuLink" data-bs-toggle="dropdown" aria-expanded="false"> Pilih Surah </a>
    <ul class="dropdown-menu" aria-labelledby="dropdownMenuLink">
      <li v-for="chapter in listSurah" :key="chapter.id">
        <router-link class="dropdown-item" :to="{ name: 'baca', params: { id: chapter.id } }">{{ chapter.name_simple }}</router-link>
      </li>
    </ul>
  </div>
  <h3>{{ surah.name_simple }}</h3>
  <h4>{{ artiSurah.name }}</h4>

  <!-- Tampilkan Ayat & Terjemah -->
  <div v-for="(ayat,index) in arrayAyat" :key="index" class="card">
    <div class="card-body">
      <h5 class="card-title">{{index+1}}{{ ayat.text_uthmani}}</h5>
      <p class="card-text">Artinya :</p>
      <p v-html="arrayTerjemahAyat[index].text"></p>
    </div>
  </div>

</template>

<script>
import axios from "axios";
import { ref } from "@vue/reactivity";
export default {
  data() {
    return {
      surah: "",
      artiSurah: "",
      arrayAyat: ref([]),
      arrayTerjemahAyat: ref([]),
      listSurah: ref([])
    };
  },
  mounted() {
    this.getAyat();
    this.getSurah();
    this.getListSurah();
    this.getTerjemahAyat();
  },
  methods: {
    getSurah() {
      axios
        .get(`https://api.quran.com/api/v4/chapters/${this.$route.params.id}?language=id`)
        .then((response) => {
          this.surah = response.data.chapter;
          this.artiSurah = this.surah.translated_name;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getAyat() {
      axios
        .get(`https://api.quran.com/api/v4/quran/verses/uthmani?chapter_number=${this.$route.params.id}`)
        .then((response) => {
          this.arrayAyat = response.data.verses;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getListSurah() {
      axios
        .get(`https://api.quran.com/api/v4/chapters?language=id`)
        .then((response) => {
          this.listSurah = response.data.chapters;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getTerjemahAyat() {
      axios
      .get(`https://api.quran.com/api/v4/quran/translations/134?chapter_number=${this.$route.params.id}`)
      .then((response) => {
        this.arrayTerjemahAyat = response.data.translations;
      })
      .catch((error) => {
        console.log(error);
      });
    }
  },
};
</script>
