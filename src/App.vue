<template>
  <div id="app">
    <header>
      <h1>My Music</h1>
    </header>
    <main>
      <section class="player">
        <!-- "{{}}" are template strings that allow us to use "data" 
        in the html. Any data change in "data" will change the
        template string -->
        <h2 class="song-title">{{current.title}}</h2>

      </section>
    </main>
  </div>
</template>

<script>
export default {
  // when we render this component it renders into the public path 
  name: 'App',
    // the "data" returns our state
  data () {
    return {
      current: {
        title: 'SONG TITLE'
      },
      songs: [
        {
          title: 'BBS',
          artist: 'Curren$y',
          src: require('./assets/01_BBS.mp3')
        },
        {
          title: 'Full Metal',
          artist: 'Curren$y',
          src: require('./assets/02_Full_Metal.mp3')
        },
        {
          title: 'The Type',
          artist: 'Curren$y',
          src: require('./assets/03_The_Type.mp3')
        },
        {
          title: 'Blood Seat And Gears',
          artist: 'Curren$y',
          src: require('./assets/04_Blood_Sweat_And_Gears_feat_Fiend.mp3')
        },
        {
          title: 'Life Instructions',
          artist: 'Curren$y',
          src: require('./assets/05_Life_Instructions.mp3')
        },
        {
          title: 'Smoke Break',
          artist: 'Curren$y',
          src: require('./assets/06_Smoke_Break.mp3')
        },
        {
          title: 'Scottie Pippens',
          artist: 'Curren$y',
          src: require('./assets/07_Scottie_Pippens.mp3')
        },
        {
          title: 'Ventilation',
          artist: 'Curren$y',
          src: require('./assets/08_Ventilation.mp3')
        },
        {
          title: 'Double 07',
          artist: 'Curren$y',
          src: require('./assets/09_Double_07.mp3')
        },
        {
          title: 'Success_Is_My_Cologne',
          artist: 'Curren$y',
          src: require('./assets/10_Success_Is_My_Cologne.mp3')
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
