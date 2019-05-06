<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <select
      v-model="selectedCountry"
      name="" id="">
      <option 
        v-for="country in countries" 
        :value="country.value">
          {{ country.name }}
        </option>
    </select>
    <spinner v-show="loading"/>
    <Artist 
      v-for="artist in artists" 
      :artist="artist" 
      :key="artist.mbid" />
  </div>
</template>

<script>
import getArtists from '../api';
import Spinner from './Spinner.vue';
import Artist from './Artist.vue';

export default {
  name: 'HelloWorld',
  data() {
    return {
      artists: [],
      countries: [
        { name: 'Colombia', value:"colombia" },
        { name: 'Argentina', value:"argentina" },
        { name: 'España', value:"spain" },
        { name: 'Alemania', value:"alemania" }
      ],
      selectedCountry: 'colombia',
      loading: true
    }
  },
  props: {
    msg: String
  },
  components: {
    Artist, 
    Spinner
  },
  methods: {
    refreshArtist() {
      const self = this;
      this.loading = true;
      this.artists = [];
      getArtists(this.selectedCountry)
        .then(function(artists) {
          self.loading = false;
          self.artists = artists
        })
    }
  },
  mounted() {
      this.refreshArtist();
  },
  watch: {
    selectedCountry() {
      this.refreshArtist();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
