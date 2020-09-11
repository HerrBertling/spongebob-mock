<template>
  <div>
    <main class="main max-w-xl m-auto pt-24 md:pt-4 pb-4 px-3">
      <h1 class="text-5xl mb-4 font-bold text-pink-500 mb-12">SpOnGeBoBiFy!</h1>
      <form class="grid grid-cols-1 gap-4 mb-12" @submit.prevent="spongify">
        <label>
          <span class="font-bold block text-lg text-gray-800">Dein Text</span>
          <input v-model="sentence" placeholder="ScHrEiB wAs…" class="border rounded-sm border-gray-400 hover:border-blue-500 focus:border-blue-500 outline-none px-4 py-3 block w-full" />
        </label>
        <div>
          <button type="submit" class="button text-white px-4 py-2 rounded-md text-lg">
            Einmal spongeboben, bitte!
          </button>
        </div>
      </form>
      <div v-if="spongedSentence" @click="copy">
        <label>
          <strong class="block text-pink-500 font-bold text-4xl mb-4">Happy trolling:</strong>
          <textarea class="h-48 bg-pink-400 rounded-md p-4 text-xl w-full block focus:outline-none mb-4" ref="copyText">
            {{ spongedSentence }}
          </textarea>
        </label>
        <p class="text-pink-500">Einfach auf's pinke Feld tippen um den Text in die Zwischenablage zu legen.</p>
      </div>
    </main>
    <footer class="max-w-xl m-auto p-4">
      <nav>
        <ul class="flex">
          <li class="mr-4">
            <a class="text-pink-400 text-sm" href="https://github.com/HerrBertling/spongebob-mock">Github</a>
          </li>
          <li>
            <a class="text-pink-400 text-sm" href="http://digitalisiering.de/">Wer hatte denn diese bekloptte Idee?</a>
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
      this.$refs.copyText.select()
      document.execCommand("copy");
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
