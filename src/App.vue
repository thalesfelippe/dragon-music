<template>
  <div id="app">
    <header>
      <i class="fas fa-dragon"></i>
      <h1>Music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">{{ current.title }} - <span>{{ current.artist }}</span></h2>
        <div class="controls">
          <button class="prev" @click="prev"><i class="fas fa-backward"></i></button>
          <button class="play" v-if="!isPlaying" @click="play"><i class="fas fa-play"></i></button>
          <button class="pause" v-else @click="pause"><i class="fas fa-pause"></i></button>
          <button class="next" @click="next"><i class="fas fa-forward"></i></button>
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
      this.player.addEventListener('ended', function () {
        this.index++;
          if (this.index > this.songs.length -1 ){
            this.index = 0;
          }

        this.current = this.songs[this.index];
        this.play(this.current);
      }.bind(this));
      this.isPlaying = true;
    },
    pause () {
      this.player.pause();
      this.isPlaying = false;
    },
    next () {
      this.index++;
      if (this.index > this.songs.length -1 ){
        this.index = 0;
      }

      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev () {
      this.index--;
      if (this.index < 0 ){
        this.index = this.songs.length -1;
      }

      this.current = this.songs[this.index];
      this.play(this.current);
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

#app {
  background-color: #C0BABC;
}

header {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  max-width: 768px;
  margin: 0 auto;
  padding: 15px;
  background-color: #011627;
  color: #FDFFFC;
}

header i {
  font-size: 50px;
  margin-top: 10px;
  color: #F71735;
}

main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
  background-color: #E5D4CE;
}

.song-title {
  color: #212121;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}

.song-title span {
  font-weight: 400;
  font-style: italic;
}

.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}

button {
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}

.play, .pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #FDFFFC;
  background-color: #F71735;
  transition: 0.4s;
}

button:hover {
  opacity: 0.9;
}

.next, .prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #FDFFFC;
  background-color: #BA1B1D;
  transition: 0.4s;
}

.playlist {
  padding: 0px 30px;
}

.playlist h3 {
  color: #011627;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}

.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}

.playlist .song:hover {
  color: #F71735;
}

.playlist .song.playing {
  color: #FFF;
  background-image: linear-gradient(to right, #BA1B1D, #F71735);
  border-radius: 20px;
  width: 75%;
  margin: 0 auto;
}
</style>
