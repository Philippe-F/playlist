<template>
  <div id="app">
    <header>
      <h1>My Music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">Test</h2>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
    // the "data" returns our state
  data () {
    return {
      current: {
        title: 'SONG TITLE'
      }
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
