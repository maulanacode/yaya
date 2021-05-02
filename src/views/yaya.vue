<template>
  <div>
    <b-container>
      <b-row>
        <b-col>
          <div>
            <digital-clock-vue
              color="#39af78"
              style="
                background: #fff;
                width: 240px;
                height: 90px;
                margin-left: auto;
                margin-right: auto;
                left: 0;
                right: 0;
              "
              class="clock"
            />
            <h1 class="mt-3">{{ datestamp }}</h1>
            <h1 class="mt-3">Hallo yaya :D</h1>
            <h2>Selamat {{ greet }} :)</h2>
            <h3 class="mt-3">Gimana nih hari kamu ? semoga baik2 aja ya :)</h3>
            <h5 class="mt-3">
              Aku punya kata2 nih buat kamu, semoga kamu suka :) <br />
              klik tombol dibawah ya :)
            </h5>

            <button
              class="btn btn-primary mt-3"
              @click="getSentence"
              v-b-modal.modal-1
            >
              untuk yaya :)
            </button>

            <b-modal id="modal-1" title="Kata-kata untuk yaya :)" ok-only>
              <p class="my-4">{{ sentence }}</p>
            </b-modal>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import DigitalClockVue from "digital-clock-vue";
export default {
  components: { DigitalClockVue },
  data() {
    return {
      timestamp: "",
      datastamp: "",
      hour: "",
      sentence: "",
      vocabulary: [
        "Tak peduli seberapa baik atau buruknya hidupmu, bangunlah setiap pagi dan bersyukurlah bahwa kamu masih memilikinya.",
        "Perpisahan hanya berlaku untuk mereka yang mencintai lewat mata. Karena untuk mereka yang mencintai dengan hati dan jiwa, tak akan ada yang namanya perpisahan.",
        "Allah menguji kita dengan sesuatu yang kita cintai, maka janganlah berlebihan mencintainya, agar saat sedih tidak berlebihan.",
        "Boleh jadi kamu membenci sesuatu padahal ia amat baik bagimu, boleh jadi pula kamu menyukai sesuatu padahal ia amat buruk bagimu. Allah mengetahui, sedang kamu tidak mengetahui.",
        "Jangan terlalu keras pada dirimu sendiri, karena hasil akhir dari semua urusan di dunia ini sudah ditetapkan oleh Allah. Jika sesuatu ditakdirkan untuk menjauh darimu, maka ia tak akan pernah mendatangimu. Namun jika ia ditakdirkan bersamamu, maka kau tak akan bisa lari darinya.",
        "Allah menguji kita dengan sesuatu yang kita cintai, maka janganlah berlebihan mencintainya, agar saat sedih tidak berlebihan.",
        "Saat Allah mengambil satu kebahagiaan yang ada padamu, Allah juga menyiapkan kebahagiaan dalam bentuk yang lain.",
        "Bila hijrahmu karena Allah, kamu akan terus melangkah walaupun sudah lelah.",
        "Tetap saling menjaga satu sama lain untuk selalu dekat dengan Allah. Semoga kelak bersama-sama masuk surga.",
        "Allah pasti akan menggantikannya dengan yang lebih baik, jika kita merelakan dia dengan ikhlas karena Allah.",
        "Pasangan paling bahagia di dunia ini tidak pernah memiliki sifat yang sama. Mereka hanya saling memahami dengan baik tentang perbedaan yang mereka miliki.",
        "Rindu tidak menuntut banyak hal. Ia hanya mengharapkan kabar dan pertemuan.",
        "Yang patah tumbuh, yang hilang berganti.",
        "Rindu terbaik adalah diam-diam mendoakan.",
        "Jatuh hati tidak bisa memilih. Tuhan memilihkan. Kita hanyalah korban. Kecewa adalah konsekuensi. Bahagia adalah bonus",
        "Tak perlu menjadi serba bisa, tekuni salah satu bidang yang kamu suka dan menjadi hebatlah dengannya.",
        "Untuk menjadi yang terbaik, kamu harus mempunyai mimpi besar serta semangat untuk mewujudkannya.",
        "Sering kali kita mengabaikan hal-hal kecil, padahal dari sanalah sesuatu yang besar lahir dan tumbuh.",
        "Kebencian adalah penyakit yang akan mematikan kebaikan.",
        "Uang memang tak menjamin kebahagian seseorang. Tapi kalau tak punya uang, kebahagiaanmu lebih tak terjamin lagi.",
        "Lebih indah hidup sederhana tapi apa adanya, daripada hidup mewah dengan hutang di mana-mana.",
        "Jika kehidupan membuat diri menangis, ingat ada ribuan kenangan indah yang membuat kita tersenyum.",
        "Cinta mungkin terkadang membuatmu rapuh, tetapi berterima kasihlah kepadanya, karena cinta darinya bsia membuatmu lebih kuat dari sebelumnya.",
        "Seberapa besar pengorbanan yang ia lakukan, maka dari situlah kita akan tahu betapa besar cintanya kepadamu.",
        "Hal yang paling penting dalam hidup adalah belajar bagaimana memberi cinta, dan membiarkannya masuk.",
        "Cinta sejati bukanlah bagaimana kamu memaafkan, tetapi bagaimana kamu melupakan, bukan apa yang kamu lihat tetapi apa yang kamu rasakan, bukan bagaimana kamu mendengarkan tetapi bagaimana kamu mengerti, dan bukan bagaimana kamu melepaskan tetapi bagaimana kamu bertahan.",
        "Hal paling indah dari persahabatan ialah memahami dan dipahami, tanpa memaksa dan ingin menang sendiri.",
        "Hidup itu pilihan, maka pilihlah sahabat yang dapat membawamu kedalam kebaikan.",
        "Ketika kamu menemukan seseorang yang bisa dipercaya, genggam erat mereka. Karena dalam hidup, sahabat sejati tak mudah ditemukan.",
        "Menyenangkan memiliki seorang sahabat yang mampu membuatmu tersenyum, meski dia sedang tak berada di sampingmu.",
        "Bila kita tidak keras terhadap kehidupan maka kehidupan yang akan bersikap keras kepada kita.",
        "Jika kamu ingin hidup yang bahagia yakinlah bahwa kamu adalah penulis cerita kehidupan kamu sendiri.",
        "Perubahan dalam hidup kamu hanya bisa terjadi jika kamu mau berubah diri kamu sendiri, bukan ketika kamu ingin menjadi orang lain yang bukan diri kamu.",
        "Suatu hal yang sia–sia jika menyesali masa lalu, sebaiknya sesalilah apa yang tak aka mampu kamu lakukan di masa depan.",
        "Jangan menyesal atas masa lalu kelam yang pernah kamu alami, yang pasti dengan masa lalu mu itu, tak peduli seburuk apapun itu ia yang bisa menjadikanmu hingga seperti sekarang ini",
        "Suatu hal yang patut menjadi kebanggaan adalah ketika seseorang memutuskan untuk menjadi dirinya sendiri.",
        "Masa depan bukanlah tujuan utama, melainkan perbaikan melalui tindakan yang benar–benar nyata.",
      ],
    };
  },
  created() {
    setInterval(this.getNow, 1000);
  },
  computed: {
    greet: function () {
      let time = this.hour;
      let result = "pagi";
      if (time >= 5 && time <= 11) {
        result = "pagi";
      } else if (time >= 11 && time <= 15) {
        result = "siang";
      } else if (time >= 15 && time <= 18) {
        result = "sore";
      } else if (time >= 18 && time <= 5) {
        result = "malam";
      } else {
        result = "";
      }
      return result;
    },
  },
  methods: {
    getSentence: function () {
      const length = this.vocabulary.length;
      const index = Math.floor(Math.random() * length);
      this.sentence = this.vocabulary[index];
    },
    getNow: function () {
      const today = new Date();
      const date =
        today.getFullYear() +
        "-" +
        (today.getMonth() + 1) +
        "-" +
        today.getDate();
      const time =
        today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
      //   const dateTime = date + " " + time;
      this.hour = today.getHours();
      this.datestamp = date;
      this.timestamp = time;
    },
  },
};
</script>

<style scoped>
/* @media (max-width: 576px) {
  .clock {
    margin-left: 50px !important;
  }
} */
</style>
