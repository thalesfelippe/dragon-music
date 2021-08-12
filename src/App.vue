<template>
  <div id="app">
    <header>
      <h1>Music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-tittle">{{ current.title }}</h2>
        {{ songs[0].src }}
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      current: {
        title: 'SONG TITTLE'
      },
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
      ]
    }
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
