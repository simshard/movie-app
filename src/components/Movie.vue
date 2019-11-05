<template>
  <v-container>
    <v-layout wrap>
      <v-flex
        xs12
        mr-1
        ml-1
      >
        <v-card>
          <v-img
            :src="singleMovie.Poster"
            aspect-ratio="2"
          />
          <v-card-title primary-title>
            <div>
              <h2 class="headline mb-0">
                {{ singleMovie.Title }}-{{ singleMovie.Year }}
              </h2>
              <p>{{ singleMovie.Plot }} </p>
              <h3>Actors: {{ singleMovie.Actors }}</h3>
              <h4>Awards: {{ singleMovie.Awards }}</h4>
              <p>Genre: {{ singleMovie.Genre }}</p>
            </div>
          </v-card-title>
          <v-card-actions>
            <v-btn
              text
              color="green"
            >
              display Ratings
            </v-btn>
            <v-btn
              text
              color="green" 
              @click="back"
            >
              back
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import axios from 'axios'
export default {
  props:{
    id:{
      type:String,
      default:''
    }
  },
  data () {
    return {
      singleMovie: '',
      dialog: false,
      loading: true,
      ratings: ''
    }
  },
  mounted () {
    const url = 'http://www.omdbapi.com/?apikey=5515fcb8&Content-Type=application/json' + '&i=' + this.id
    axios
      .get(url)
      .then(response => {
        this.singleMovie = response.data
        this.ratings = this.singleMovie.Ratings
        this.loading = false
      })
      .catch(error => {
        console.log(error)
      })
  },
  methods: {
    back () {
      this.$router.push('/')
    }
  }
}

</script>

<style  scoped>
  .v-progress-circular
  {  margin: 1rem;}
</style>