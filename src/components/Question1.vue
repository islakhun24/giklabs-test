<template>
  <div class="col-12 col-md-4 card shadow p-3 justify-content-start">
    <h1 class="text-center">Question 1</h1>
    <div class="mt-3">
      <form @submit.prevent="submitForm()">
        <div class="mb-3">
          <label for="exampleFormControlInput1" class="form-label">Masukan Strings</label>
          <input type="text" class="form-control" v-model="formData.strings" id="exampleFormControlInput1" placeholder="Masukan String ...">
        </div>
        <div class="mb-3">
          <label for="exampleFormControlInput1" class="form-label">Masukan Query</label>
          <input type="text" class="form-control" v-model="formData.query" id="exampleFormControlInput1" placeholder="Masukan Query ...">
        </div>
        <button class="btn btn-primary w-100" type="submit">Submit</button>
      </form>
    </div>
    <div v-if="result" class="mt-3">
      <h6>Hasil</h6>
      <pre>{{result}}</pre>
    </div>
  </div>
</template>

<script>
export default {
  name: 'QuestionOne',
  data: () => ({
    formData: {
      strings: 'abbcccd',
      query: '1,3,9,8'
    },
    result: null
  }),

  methods: {
     weightedStrings: function (string, queries) {
       // Inisialisasi bobot karakter
       const weights = {
         a: 1, b: 2, c: 3, d: 4, e: 5, f: 6, g: 7, h: 8, i: 9, j: 10, k: 11, l: 12,
         m: 13, n: 14, o: 15, p: 16, q: 17, r: 18, s: 19, t: 20, u: 21, v: 22,
         w: 23, x: 24, y: 25, z: 26
       };

       // Membuat objek kosong tanpa mewarisi properti dari Object.prototype
       const weightsCache = Object.create(null);

       // Fungsi untuk menghitung bobot substring
       function calculateSubstringWeight(substring) {
         // Jika bobot substring sudah pernah dihitung, kembalikan dari cache
         if (substring in weightsCache) {
           return weightsCache[substring];
         }

         let weight = 0;
         // Menghitung bobot substring dengan menjumlahkan bobot karakter-karakternya
         for (let i = 0; i < substring.length; i++) {
           weight += weights[substring[i]];
         }

         // Menyimpan bobot substring ke cache
         weightsCache[substring] = weight;
         return weight;
       }

       const results = [];

       // Melakukan iterasi untuk setiap query
       for (let i = 0; i < queries.length; i++) {
         const query = queries[i];
         let j = 0;
         let found = false;

         // Melakukan iterasi pada string
         while (j < string.length) {
           let substring = '';
           let k = j;

           // Membentuk substring dengan karakter-karakter berurutan yang sama
           while (k < string.length && string[k] === string[j]) {
             substring += string[k];

             // Menghitung bobot substring dan membandingkannya dengan query
             const weight = calculateSubstringWeight(substring);

             // Jika bobot substring sama dengan query, tambahkan 'Yes' ke hasil dan tandai sebagai ditemukan
             if (weight === query) {
               results.push('Yes');
               found = true;
               break;
             }

             k++;
           }

           // Jika sudah ditemukan, keluar dari loop
           if (found) {
             break;
           }

           j++;
         }

         // Jika tidak ditemukan, tambahkan 'No' ke hasil
         if (!found) {
           results.push('No');
         }
       }

       return results;
    },
     submitForm() {
      // Lakukan sesuatu dengan data yang di-submit
       const newQuery = this.formData.query.split(",").map(Number);
       this.result = this.weightedStrings(this.formData.strings, newQuery)
    }
  },
}
</script>

<style scoped>

</style>
