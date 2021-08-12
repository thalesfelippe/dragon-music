<template>
  <div id="app">
    <header>
      <h1>Music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-tittle">{{ current.title }} - <span>{{ current.artist }}</span></h2>
        <div class="control">
          <button class="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>Playlist</h3>
        <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing' : 'song'">
          {{ song.title }} - {{ song.artist }}
        </button>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: 'Fight Back',
          artist: 'Neffex',
          src: require('./assets/neffex-fight-back.mp3')
        },
        {
          title: 'Careless',
          artist: 'Neffex',
          src: require('./assets/neffex-careless.mp3')
        },
        {
          title: 'Destiny',
          artist: 'Neffex',
          src: require('./assets/neffex-destiny.mp3')
        },
        {
          title: 'Never Give Up',
          artist: 'Neffex',
          src: require('./assets/neffex-never-give-up.mp3')
        },
        {
          title: 'Rumors',
          artist: 'Neffex',
          src: require('./assets/neffex-rumors.mp3')
        },
        {
          title: 'Soldier',
          artist: 'Neffex',
          src: require('./assets/neffex-soldier.mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods: {
    play (song) {
      if (typeof song.src != "undefined") {
        this.current = song;

        this.player.src = this.current.src;
      }

      this.player.play();
      this.isPlaying = true;
    },
    pause () {
      this.player.pause();
      this.isPlaying = false;
    }
  },
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    this.player.play();
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #FFF;
}
</style>
