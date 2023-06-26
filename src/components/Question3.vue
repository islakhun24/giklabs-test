<template>
  <div class="col-12 col-md-4 card shadow p-3 justify-content-start">
    <h1 class="text-center">Question 2</h1>
    <div class="mt-3">
      <form @submit.prevent="submitForm()">
        <div class="mb-3">
          <label for="exampleFormControlInput1" class="form-label">Masukan Sample 1</label>
          <input type="text" class="form-control" v-model="formData.sample1" id="exampleFormControlInput1" placeholder="Masukan Sample 1 ...">
        </div>
        <div class="mb-3">
          <label for="exampleFormControlInput1" class="form-label">Masukan Sample 2</label>
          <input type="text" class="form-control" v-model="formData.sample2" id="exampleFormControlInput1" placeholder="Masukan Sample 2 ...">
        </div>
        <div class="mb-3">
          <label for="exampleFormControlInput1" class="form-label">Masukan Sample 3</label>
          <input type="text" class="form-control" v-model="formData.sample3" id="exampleFormControlInput1" placeholder="Masukan Sample 3 ...">
        </div>
        <button class="btn btn-primary w-100" type="submit">Submit</button>
      </form>
    </div>
    <div v-if="result" class="mt-3">
      <h6>Hasil</h6>
      <pre v-if="result.sample1">Sample 1: {{result.sample1}}</pre>
      <pre v-if="result.sample2">Sample 2: {{result.sample2}}</pre>
      <pre v-if="result.sample3">Sample 3: {{result.sample3}}</pre>
    </div>
  </div>
</template>

<script>
export default {
  name: 'QuestionOne',
  data: () => ({
    formData: {
      sample1: '{[()]}',
      sample2: '{[(])}',
      sample3: '{(([])[])[]}',
    },
    result: {
      sample1: null,
      sample2: null,
      sample3: null,
    }
  }),

  methods: {
    isBalancedBracket: function (input) {
      const stack = []; // Membuat tumpukan (stack) untuk menyimpan tanda kurung buka

      for (let i = 0; i < input.length; i++) {
        const char = input[i];

        if (char === '(' || char === '{' || char === '[') {
          stack.push(char); // Jika karakter adalah tanda kurung buka, tambahkan ke dalam tumpukan
        } else if (char === ')' || char === '}' || char === ']') {
          if (stack.length === 0) {
            return 'NO'; // Jika tumpukan kosong saat ditemui tanda kurung tutup, maka tidak seimbang
          }

          const top = stack.pop(); // Mengambil tanda kurung buka teratas dari tumpukan

          if (
              (char === ')' && top !== '(') || // Periksa kecocokan antara tanda kurung buka dan tutup
              (char === '}' && top !== '{') ||
              (char === ']' && top !== '[')
          ) {
            return 'NO'; // Jika tidak cocok, tidak seimbang
          }
        }
      }

      if (stack.length === 0) {
        return 'YES'; // Jika tumpukan kosong setelah memeriksa semua karakter, maka seimbang
      } else {
        return 'NO'; // Jika masih ada tanda kurung buka yang tersisa di tumpukan, tidak seimbang
      }
    },
    submitForm() {
      // Lakukan sesuatu dengan data yang di-submit
      this.result.sample1 = this.isBalancedBracket(this.formData.sample1)
      this.result.sample2 = this.isBalancedBracket(this.formData.sample2)
      this.result.sample3 = this.isBalancedBracket(this.formData.sample3)
    }
  },
}
</script>

<style scoped>

</style>
