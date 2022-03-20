<template>
  <div>
    <main class="main max-w-xl m-auto pt-24 md:pt-4 pb-4 px-3">
      <h1 class="text-5xl font-bold text-pink-500 mb-12">SpOnGeBoBiFy!</h1>
      <form class="grid grid-cols-1 gap-4 mb-12" @submit.prevent="spongify">
        <label>
          <span class="font-bold block text-xl text-pink-500 mb-2">Your text</span>
          <input v-model="sentence" placeholder="WrItE sOmEtHiNg…" class="border rounded-sm border-gray-400 hover:border-blue-500 focus:border-blue-500 outline-none px-4 py-3 mb-4 block w-full" />
        </label>
        <div>
          <button type="submit" class="text-white bg-pink-500 px-4 py-2 rounded-md text-lg hover:bg-pink-700 active:bg-pink-700 focus:bg-pink-700 transition-colors">
            SpOnGeBoBiFy, PlEaSe!
          </button>
        </div>
      </form>
      <div v-if="spongedSentence" @click="copy">
        <label>
          <strong class="block text-pink-500 font-bold text-4xl mb-4">Happy trolling:</strong>
          <textarea class="h-48 bg-pink-300 rounded-md p-4 text-xl w-full block focus:outline-none mb-4 text-pink-900" ref="copyText" readonly>{{ spongedSentence }}</textarea>
        </label>
        <p class="text-pink-400">Just click the pink field to copy the text to your clipboard.</p>
      </div>
    </main>
    <footer class="max-w-xl m-auto p-4">
      <nav>
        <ul class="flex">
          <li class="mr-4">
            <a class="text-pink-400 text-sm" href="https://github.com/HerrBertling/spongebob-mock">Github</a>
          </li>
          <li>
            <a class="text-pink-400 text-sm" href="http://digitalisiering.de/">Who had this stupid idea?</a>
          </li>
        </ul>
      </nav>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App',

  data() {
    return {
      sentence: '',
      previousLetter: null,
      case: 'uppercase',
      spongedSentence: ''
    }
  },

  methods: {
    isLetter(letter) {
      const regex = new RegExp('[a-zA-Z]')
      return regex.test(letter)
    },

    spongify() {
      this.spongedSentence = this.sentence.split('').map((letter) => {
        if (!this.isLetter(letter)) {
          return letter
        }
        if (this.case === 'uppercase') {
          this.case = 'lowercase'
          return letter.toUpperCase()
        }
        this.case = 'uppercase'
        return letter.toLowerCase()
      }).join('')
      this.case = 'uppercase'
    },

    copy() {
      this.$refs.copyText.select();
      document.execCommand('copy');
    }
  }
}
</script>

<style scoped>
.main {
  min-height: 90vh;
}
.button {
  background-color: #26B9C8;
}

.button:hover,
.button:focus,
.button:active {
  background-color: #0457A0;
}

</style>
