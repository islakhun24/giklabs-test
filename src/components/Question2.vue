<template>
  <div class="col-12 col-md-4 card shadow p-3 justify-content-start">
    <h1 class="text-center">Question 2</h1>
    <div class="mt-3">
      <form @submit.prevent="submitForm()">
        <div class="mb-3">
          <label for="exampleFormControlInput1" class="form-label">Masukan Strings</label>
          <input type="text" class="form-control" v-model="formData.strings" id="exampleFormControlInput1" placeholder="Masukan String ...">
        </div>
        <div class="mb-3">
          <label for="exampleFormControlInput1" class="form-label">K</label>
          <input type="text" class="form-control" v-model="formData.k" id="exampleFormControlInput1" placeholder="Masukan K ...">
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
      strings: '3943',
      k: '1'
    },
    result: null
  }),

  methods: {
    highestPalindrome: function (string, k) {
      // Mengecek apakah string merupakan palindrome
      function isPalindrome(str) {
        if (str.length <= 1) {
          return true;
        }

        if (str[0] !== str[str.length - 1]) {
          return false;
        }

        return isPalindrome(str.slice(1, str.length - 1));
      }

      // Mengganti karakter pada posisi tertentu dalam string
      function replaceCharAt(str, index, char) {
        return str.substring(0, index) + char + str.substring(index + 1);
      }

      // Mencari highest palindrome dengan melakukan rekursi
      function findHighestPalindrome(str, k) {
        // Basis: jika k = 0, cek apakah string merupakan palindrome
        if (k === 0) {
          if (isPalindrome(str)) {
            return str;
          } else {
            return -1;
          }
        }

        // Jika k > 0, cari posisi pertama dan terakhir yang berbeda
        let firstDiffIndex = -1;
        let lastDiffIndex = -1;
        for (let i = 0; i < Math.floor(str.length / 2); i++) {
          if (str[i] !== str[str.length - 1 - i]) {
            firstDiffIndex = i;
            lastDiffIndex = str.length - 1 - i;
            break;
          }
        }

        // Jika tidak ada perbedaan, maka string sudah palindrome
        if (firstDiffIndex === -1) {
          return str;
        }

        // Mengganti karakter pada posisi pertama dengan karakter pada posisi terakhir
        const palindrome1 = replaceCharAt(str, firstDiffIndex, str[lastDiffIndex]);
        // Mengganti karakter pada posisi terakhir dengan karakter pada posisi pertama
        const palindrome2 = replaceCharAt(str, lastDiffIndex, str[firstDiffIndex]);

        // Lanjutkan rekursi dengan k - 1 untuk mencari highest palindrome baru
        const result1 = findHighestPalindrome(palindrome1, k - 1);
        const result2 = findHighestPalindrome(palindrome2, k - 1);

        // Membandingkan hasil rekursi dan mengembalikan highest palindrome yang lebih besar
        if (result1 === -1) {
          return result2;
        } else if (result2 === -1) {
          return result1;
        } else {
          return result1 > result2 ? result1 : result2;
        }
      }

      return findHighestPalindrome(string, k);
    },
    submitForm() {
      // Lakukan sesuatu dengan data yang di-submit
      this.result = this.highestPalindrome(this.formData.strings, this.formData.k)
    }
  },
}
</script>

<style scoped>

</style>
