<template>
  <div class="container">
    <div id="practice">
      <h2 class="subtitle">
        {{ description }}
      </h2>
      <div v-if="message === 'root'" class="button--grey" @click="ring_root">
        ルート音を聴く
      </div>
      <div
        v-if="message === 'interval'"
        class="button--grey"
        @click="ring_interval"
      >
        ２つ目の音を聴く
      </div>
      <div v-if="message === 'answer'">
        <div
          v-for="(interval, index) in intervals"
          :key="interval"
          class="button--grey"
          @click="check_answer(index)"
        >
          {{ interval }}
        </div>
      </div>
      <div class="bottom">
        <div v-if="message === 'answer'" class="button--green" @click="restart">
          次の問題
        </div>
        <nuxt-link to="/" class="button--grey">
          トップへ
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
// import NoteButton from '~/components/NoteButton.vue'
var Tone = require('tone')
export default {
  data: function() {
    return {
      description: '音を聞いてみよう',
      message: 'root',
      intervals: [
        'm2',
        'M2',
        'm3',
        'M3',
        'P4',
        'TT',
        'P5',
        'm6',
        'M6',
        'm7',
        'M7'
      ],
      second_note_interval: null
    }
  },
  methods: {
    ring_root: function() {
      var synth = new Tone.Synth().toMaster()

      synth.triggerAttackRelease('C4', '2n')
      this.message = 'interval'
    },
    ring_interval: function() {
      var synth = new Tone.Synth().toMaster()
      var notes = [
        'C#4',
        'D4',
        'D#4',
        'E4',
        'F4',
        'F#4',
        'G4',
        'G#4',
        'A4',
        'A#4',
        'B4'
      ]
      var note = notes[Math.floor(Math.random() * notes.length)]

      synth.triggerAttackRelease(note, '2n')
      this.second_note_interval = notes.indexOf(note) + 2
      this.second_note = note
      this.message = 'answer'
      this.description = '二つの音はどんな関係？'
    },
    check_answer: function(index) {
      var answer_interval = index + 2
      if (answer_interval === this.second_note_interval) {
        this.description =
          '正解!!' +
          ' C4と' +
          this.second_note +
          'の関係は' +
          this.intervals[this.second_note_interval - 2] +
          'です。'
      } else {
        this.description =
          '不正解!!' +
          ' C4と' +
          this.second_note +
          'の関係は' +
          this.intervals[this.second_note_interval - 2] +
          'です。'
      }
    },
    restart: function() {
      this.message = 'root'
      this.description = '音を聞いてみよう'
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.subtitle {
  font-weight: 300;
  font-size: 22px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

.bottom {
  padding-top: 50px;
}
</style>
