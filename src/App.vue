<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        Mooovie 
      </div>
      <v-spacer /> 
      <v-flex 
        xs12
        sm6
        md3
      >
        <v-text-field
          v-model="searchString"
          label="Movie Name"
        />
      </v-flex>
      <v-btn
        text
        :disabled="!dataAvailable"
        @click="searchMovie"
      >
        <span class="mr-2">Search</span>
      </v-btn>
    </v-app-bar>
    <v-content>
      <router-view />
    </v-content>
  </v-app>
</template>

<script>
export default {
  name: 'App',
  components: {
  },
  data () {
    return {
      searchString: ''
    }
  },
  computed: {
    dataAvailable () {
      return this.searchString !== null && this.searchString !== ''
    }
  },
  methods: {
    searchMovie () {
      this.$router.push('/search/' + this.searchString)
      this.searchString = ''
    }
  }
}
</script>
