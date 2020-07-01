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
        <h2 class="song-title">{{ current.title }} - <span>{{ current.artist }}</span></h2>
        <div class="controls">
          <!-- "v-if" is a vue conditional used to conditionally render a block. 
          The block will only be rendered if the directive’s expression returns 
          a truthy value -->
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>The Playlist</h3>
        <!-- Loop thorugh the songs array and create buttons for each song in the array.
        The "@click" makes each button clickable and plays the song. 
        The (song.src == current.src) ? 'song playing' : 'song' ternary binds the 
        button to a different class depending on if the song is playing, which allows 
        us to style it differently if it is playing.  -->
        <button v-for="song in songs" :key="song.src" @click=play(song) 
        :class="(song.src === current.src) ? 'song playing' : 'song'">
          {{song.title}} - {{song.artist}}
        </button>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  // when we render this component it renders into the public path, gives all
  // songs a media path 
  name: 'App',
    // the "data" returns our state
  data () {
    return {
      current: {},
      index: 0,
      isPlaying: false,
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
          title: 'Success Is My Cologne',
          artist: 'Curren$y',
          src: require('./assets/10_Success_Is_My_Cologne.mp3')
        },
        {
          title: 'Holy Ghost',
          artist: 'Rick Ross',
          src: require('./assets/01_Holy_Ghost.mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods: {
    async play(song) {
    //  When you click play the @click triggers a MouseOverEvent. MOE do not have 
    //  "src" so this if statement sets the current song and index
      if (typeof song.src !== 'undefined') {
        this.current = song;
        this.index = this.songs.indexOf(this.current);

        this.player.src = this.current.src;
      }
      
      this.player.play()
      .then()
      .catch((err) => console.log(err))
      this.isPlaying = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }

      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }

      this.current = this.songs[this.index];
      this.play(this.current);

    }
  },
  // This is a lifecycle method. As soon as the app gets created this method is run

  // we must use "this" to gain access to the "data" object
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src; 
    this.player.addEventListener('ended', () => { this.next() });
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

main {
width: 100%;
max-width: 768px;
margin: 0 auto;
padding: 25px;
}

.song-title {
  color: #53565A;
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
  cursor: pointer;
}

.play, .pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #FFF;
  background-color: #CC2E5D;
}

.next, .prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #FFF;
  background-color: #FF5858;
}

.playlist {
  padding: 0px 30px;
  color: #212121;
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
  color: #FF5858;
}

.playlist .song.playing {
  color: #FFF;
  background-image: linear-gradient(to right, #CC2E5D, #FF5858);
}

</style>
